# Save 30-40% on LLM Costs with Semantic Caching: A Step-by-Step Guide

## What We're Building

A highly optimized AI application that:
- Routes requests through Portkey's AI Gateway
- Caches identical queries to speed up responses and eliminate API costs entirely
- Uses embedding-based "Semantic Caching" to recognize when differently-worded prompts mean the exact same thing
- Enforces a Time-To-Live (TTL) cache expiration

By the end, you will have an architecture capable of shaving $1,000s off your monthly LLM invoices.

## Why This Matters

At Portkey, we process over 125M daily requests and track $500K+ in daily AI spend. We've discovered a shocking metric: **In many enterprise deployments, up to 40% of all API requests are functionally identical to a query made within the last hour.**

Whether it's an e-commerce chatbot answering "What is your refund policy?" or a data pipeline parsing a standardized document template, developers are paying OpenAI and Anthropic repeatedly to generate the exact same tokens.

Caching an LLM response at the edge eliminates that cost and drops response latency into the low milliseconds. 

## Prerequisites

- Python 3.9+
- Portkey account (free at [app.portkey.ai](https://app.portkey.ai))
- OpenAI API key or Anthropic API key

## Step 1: Install & Setup

First, let's install the Portkey SDK and initialize our standard connection.

```bash
pip install portkey-ai
```

```python
import os
import time
from portkey_ai import Portkey

# Initialize Portkey
client = Portkey(
    api_key=os.getenv("PORTKEY_API_KEY"),
    provider="openai",
    Authorization=os.getenv("OPENAI_API_KEY")
)

def time_request(prompt: str):
    """A helper function to measure latency."""
    start = time.time()
    response = client.chat.completions.create(
        model="gpt-4o-mini",
        messages=[{"role": "user", "content": prompt}]
    )
    end = time.time()
    print(f"⏱️ Took {end-start:.2f} seconds")
    print(f"💬 Response: {response.choices[0].message.content}\\n")
    return response

# Standard direct API call (uncached)
print("Standard Request:")
time_request("List the three largest planets in the solar system.")
```

*Output:*
```text
Standard Request:
⏱️ Took 1.84 seconds
💬 Response: The three largest planets...
```

Right now, this took almost 2 seconds and incurred an API cost based on token usage. Let's fix that.

## Step 2: Implement Simple Caching

"Simple Caching" guarantees that if the *exact* string of text is received again, the cached response is served.

```python
# Define a simple caching configuration
simple_cache_config = {
    "cache": {
        "mode": "simple",
        # Cache expires in 3600 seconds (1 hour)
        "max_age": 3600 
    }
}

# Apply the config to the client
simple_cache_client = client.with_options(config=simple_cache_config)

def time_simple_request(prompt: str):
    start = time.time()
    response = simple_cache_client.chat.completions.create(
        model="gpt-4o-mini",
        messages=[{"role": "user", "content": prompt}]
    )
    end = time.time()
    print(f"⏱️ Took {end-start:.2f} seconds")
    return response

print("First Cached Call (Cache Miss - routing to OpenAI):")
time_simple_request("What is the capital of Japan?")

print("\\nSecond Cached Call (Cache Hit - served from Portkey Edge):")
time_simple_request("What is the capital of Japan?")
```

*Output:*
```text
First Cached Call (Cache Miss - routing to OpenAI):
⏱️ Took 1.21 seconds

Second Cached Call (Cache Hit - served from Portkey Edge):
⏱️ Took 0.04 seconds
```

✅ **That's a 96% reduction in latency and a 100% reduction in API cost for the second query.**

## Step 3: Implement Semantic Caching

Simple caching is great, but human users rarely type the exact same sequence of characters. 
- User 1: "What's Japan's capital?"
- User 2: "Tell me the capital city of Japan."

These are functionally identical, but a Simple Cache treats them differently. 

Semantic Caching uses high-speed vector embeddings to calculate the mathematical similarity between the current prompt and cached prompts. If the similarity surpasses a threshold, it serves the cached response.

```python
# Define semantic caching configuration
semantic_cache_config = {
    "cache": {
        "mode": "semantic",
        "max_age": 3600
    }
}

semantic_client = client.with_options(config=semantic_cache_config)

def time_semantic_request(prompt: str):
    start = time.time()
    response = semantic_client.chat.completions.create(
        model="gpt-4o-mini",
        messages=[{"role": "user", "content": prompt}]
    )
    end = time.time()
    print(f"⏱️ Took {end-start:.2f} seconds | Prompt: '{prompt}'")
    return response

print("First Semantic Call (Cache Miss - populating vector db):")
time_semantic_request("Can you tell me the fastest land animal?")

print("\\nSecond Semantic Call (Different string, same meaning -> Cache Hit!):")
time_semantic_request("What is the quickest animal on land?")

print("\\nThird Semantic Call (Different string, same meaning -> Cache Hit!):")
time_semantic_request("Name the land animal that runs the fastest.")
```

*Output:*
```text
First Semantic Call (Cache Miss - populating vector db):
⏱️ Took 1.45 seconds | Prompt: 'Can you tell me the fastest land animal?'

Second Semantic Call (Different string, same meaning -> Cache Hit!):
⏱️ Took 0.12 seconds | Prompt: 'What is the quickest animal on land?'

Third Semantic Call (Different string, same meaning -> Cache Hit!):
⏱️ Took 0.11 seconds | Prompt: 'Name the land animal that runs the fastest.'
```

Both the second and third queries were intercepted by the Semantic Cache, saving you the round-trip and generation cost to OpenAI!

## Complete Code

Here's the full production-ready implementation, combining Semantic Caching with Portkey's Automatic Fallbacks for ultimate reliability:

```python
import os
import time
from portkey_ai import Portkey

# Initialize Portkey
client = Portkey(api_key=os.getenv("PORTKEY_API_KEY"))

# Enterprise Configuration: Semantic Cache + Fallbacks
enterprise_config = {
    "strategy": {"mode": "fallback"},
    "targets": [
        {
            "provider": "openai",
            "Authorization": os.getenv("OPENAI_API_KEY"),
            "override_params": {"model": "gpt-4o-mini"}
        },
        {
            "provider": "anthropic",
            "Authorization": os.getenv("ANTHROPIC_API_KEY"),
            "override_params": {"model": "claude-3-5-haiku-20241022"}
        }
    ],
    "cache": {
        "mode": "semantic",
        "max_age": 86400  # 24 hour TTL
    }
}

enterprise_client = client.with_options(config=enterprise_config)

def query_ai(prompt: str):
    start = time.time()
    response = enterprise_client.chat.completions.create(
        messages=[{"role": "user", "content": prompt}]
    )
    print(f"Response: {response.choices[0].message.content[:50]}...")
    print(f"Latency: {time.time()-start:.2f}s\\n")

# Run
query_ai("Summarize the theory of relativity in one sentence.")
query_ai("In a single sentence, explain Einstein's relativity theory.")
```

## What's Next

Deploying Semantic Caching is the fastest way to drop your LLM infrastructure bills. When Portkey raised our $15M Series A, it was precisely because we make optimization architectures like this accessible with just JSON configs.

- **Explore Tracing**: [Trace these cached requests in your Dashboard](https://portkey.ai/docs/product/observability)
- **Implement Guardrails**: [Block unsafe inputs on cached misses](https://portkey.ai/docs/product/guardrails)
- **Manage Prompts**: [Version and test prompts before deployment](https://portkey.ai/docs/product/prompt-library)

---

⭐ Star the gateway: [github.com/Portkey-AI/gateway](https://github.com/Portkey-AI/gateway)

---

## Metadata
- **Title**: Save 30-40% on LLM Costs with Semantic Caching: A Step-by-Step Guide
- **Tags**: LLMs, Cost Optimization, Semantic Caching, Python, Vector DB
- **Read time**: 6 minutes
