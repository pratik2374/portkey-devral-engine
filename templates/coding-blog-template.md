# Coding Blog Template

Use this structure when generating tutorial-style coding blogs for Portkey AI — step-by-step builds that take the reader from zero to a working implementation.

---

## File Structure

```markdown
# [Title]: A Step-by-Step Guide

## What We're Building
[Screenshot or description of the end result]

## Why This Matters
[1-2 paragraphs on the production AI problem this solves]

## Prerequisites
[What you need before starting]

## Step 1: [Setup]
[Code + explanation]

## Step 2: [Core Feature]
[Code + explanation]

## Step 3-N: [Build progressively]
[Code + explanation]

## Complete Code
[Full working code in one block]

## What's Next
[Extensions and improvements]

---

## Metadata
- **Title**: [Title]
- **Tags**: [tags]
- **Read time**: [X] minutes
```

---

## Writing Guidelines

### Tone
- Conversational, like pair programming
- "Let's build..." and "Now we'll add..."
- Celebrate progress: "That's it! You've just..."

### Structure
- Each step adds exactly one feature/concept
- Every step has runnable code
- Show output/results after each step
- Build towards a complete solution

### Code Blocks
- Include comments for key lines
- Show terminal output where relevant
- Highlight Portkey-specific code with comments

---

## Sample Blog Structure

```markdown
# Build a Reliable AI Chatbot with Automatic Fallbacks: A Step-by-Step Guide

## What We're Building

A production-ready AI chatbot that:
- Routes requests through Portkey's AI Gateway
- Automatically falls back to a backup LLM if the primary goes down
- Logs every request for observability
- Caches repeated queries to save costs

By the end, you'll have a chatbot that stays up even when your LLM provider doesn't.

## Why This Matters

In production, LLM API reliability is everything. A single provider outage can take down your entire AI feature. Portkey solves this by acting as an intelligent gateway between your app and LLM providers.

## Prerequisites

- Python 3.9+
- Portkey account (free at [app.portkey.ai](https://app.portkey.ai))
- OpenAI API key
- Anthropic API key (for fallback)

## Step 1: Install & Setup

Install the Portkey SDK:

```bash
pip install portkey-ai
```

Set up your environment variables:

```bash
export PORTKEY_API_KEY="your-portkey-key"
export OPENAI_API_KEY="your-openai-key"
export ANTHROPIC_API_KEY="your-anthropic-key"
```

Initialize the client:

```python
import os
from portkey_ai import Portkey

client = Portkey(
    api_key=os.getenv("PORTKEY_API_KEY"),
    provider="openai",
    Authorization=os.getenv("OPENAI_API_KEY")
)

# Quick test
response = client.chat.completions.create(
    model="gpt-4o",
    messages=[{"role": "user", "content": "Hello!"}]
)
print(response.choices[0].message.content)
# Output: Hello! How can I help you today?
```

✅ You've just routed your first request through Portkey's AI Gateway!

## Step 2: Add Automatic Fallbacks

Now let's make it resilient. If OpenAI goes down, we'll auto-switch to Anthropic:

```python
fallback_config = {
    "strategy": {"mode": "fallback"},
    "targets": [
        {
            "provider": "openai",
            "override_params": {"model": "gpt-4o"},
            "Authorization": os.getenv("OPENAI_API_KEY")
        },
        {
            "provider": "anthropic",
            "override_params": {"model": "claude-sonnet-4-20250514"},
            "Authorization": os.getenv("ANTHROPIC_API_KEY")
        }
    ]
}

# Apply the config
resilient_client = client.with_options(config=fallback_config)
```

That's it — if OpenAI returns an error, Portkey automatically retries with Claude. No try/catch needed.

## Step 3: Add Guardrails

Let's add output validation to ensure safe responses:

```python
guarded_config = {
    **fallback_config,
    "retry": {"attempts": 3},
    "output_guardrails": [{
        "default.contains": {
            "operator": "none",
            "words": ["harmful_content"]
        },
        "deny": True
    }]
}

safe_client = client.with_options(config=guarded_config)
```

Now every response is validated before reaching your users.

## Step 4: Build the Chat Function

Let's wrap everything in a clean function:

```python
def chat(user_message: str, history: list = None) -> str:
    """Send a message through Portkey with fallbacks and guardrails."""
    if history is None:
        history = []
    
    messages = [
        {"role": "system", "content": "You are a helpful assistant."},
        *history,
        {"role": "user", "content": user_message}
    ]
    
    response = safe_client.chat.completions.create(
        messages=messages
    )
    
    return response.choices[0].message.content

# Try it!
print(chat("What is an AI Gateway?"))
```

## Complete Code

Here's the full implementation in one block:

```python
import os
from portkey_ai import Portkey

# Initialize Portkey
client = Portkey(api_key=os.getenv("PORTKEY_API_KEY"))

# Config with fallbacks + guardrails
config = {
    "strategy": {"mode": "fallback"},
    "targets": [
        {
            "provider": "openai",
            "override_params": {"model": "gpt-4o"},
            "Authorization": os.getenv("OPENAI_API_KEY")
        },
        {
            "provider": "anthropic",
            "override_params": {"model": "claude-sonnet-4-20250514"},
            "Authorization": os.getenv("ANTHROPIC_API_KEY")
        }
    ],
    "retry": {"attempts": 3},
    "output_guardrails": [{
        "default.contains": {
            "operator": "none",
            "words": ["harmful_content"]
        },
        "deny": True
    }]
}

safe_client = client.with_options(config=config)

def chat(user_message: str, history: list = None) -> str:
    messages = [
        {"role": "system", "content": "You are a helpful assistant."},
        *(history or []),
        {"role": "user", "content": user_message}
    ]
    response = safe_client.chat.completions.create(messages=messages)
    return response.choices[0].message.content

# Run
print(chat("What makes an AI app production-ready?"))
```

## What's Next

- **Add semantic caching**: [Save 30-40% on API costs](https://portkey.ai/docs/product/ai-gateway/cache-simple-and-semantic)
- **Deploy with MCP Gateway**: [Manage MCP servers](https://portkey.ai/docs/product/mcp-gateway)
- **Monitor in dashboard**: [Analyze requests and metadata](https://portkey.ai/docs/product/observability)
- **Manage Prompts**: [Version and test prompts in the Studio](https://portkey.ai/docs/product/prompt-library)

---

⭐ Star the gateway: [github.com/Portkey-AI/gateway](https://github.com/Portkey-AI/gateway)
```

---

## File Naming

Format: `{bucket}-{short-title}-tutorial.md`

Examples:
- `gateway-resilient-chatbot-tutorial.md`
- `observability-custom-metadata-tutorial.md`
- `prompt-management-versioning-tutorial.md`
- `getting-started-first-app-tutorial.md`
- `advanced-semantic-caching-tutorial.md`
