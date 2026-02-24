# How We Saved Customers Millions After Raising Our $15M Series A

## TL;DR

Generative AI is expensive, and unoptimized API usage is bleeding enterprise budgets dry. By deploying Portkey's AI Gateway, our customers have saved millions of dollars through granular cost analytics, budget caps, and semantic caching. Here is the architecture allowing us to manage over $500K in daily AI spend across 125M daily requests.

## The Problem

When a new LLM application goes into production, the architecture usually looks like a straight line: Application code talks directly to the OpenAI (or Anthropic) API. 

For the first few weeks, this works fine. But as usage scales to hundreds of thousands of requests, the cracks begin to show, particularly at the end of the month when the API bill arrives. Engineering teams are handed a massive invoice with absolutely no context. 

- "Which customer generated $4,000 of GPT-4o usage yesterday?"
- "Did our new 'Document Summarization' feature cause this latency spike?"
- "Are we paying twice to generate the exact identical response for different users?"

Without an observability layer between your application and the LLM provider, answering these questions requires weeks of custom monitoring engineering. 

We raised our $15M Series A specifically to solve this visibility problem at an infrastructural level. Portkey is the unified control plane that sits between your code and your models, providing the cost tracking and optimization tools that generic APM providers (like Datadog) miss because they don't understand native LLM payloads.

## How Cost Optimization Works at the Gateway

Cost optimization isn't just about finding cheaper models; it's about eliminating waste. Portkey tackles this through three distinct gateway mechanisms:

1. **Granular Metadata Tagging**: Every request is tagged with identifiers (e.g., `user_id`, `environment`, `feature`). The cost of the prompt and completion tokens is calculated in real-time and attributed to these specific tags.
2. **Budget Enforcement**: Hard limits are set on these tags at the gateway level. If `user_id_1092` exceeds their $50 monthly LLM budget, the gateway blocks the request *before* it reaches the expensive provider API.
3. **Semantic Caching**: The gateway intercepts the request and calculates a vector embedding of the prompt. If a mathematically identical (or highly similar) prompt was recently processed, the gateway returns the cached response in milliseconds—saving 100% of the inference cost.

## Architecture

```mermaid
graph TD
    A[Your Application] -->|1. Request with Metadata| B((Portkey AI Gateway))
    
    B -->|2. Check Cache| C{Cache Hit?}
    C -- Yes -->|3a. Return Cached Response in 15ms| A
    
    C -- No --> D{Budget Exceeded?}
    D -- Yes -->|3b. Block Request HTTP 402| A
    
    D -- No --> E[Route to OpenAI/Anthropic]
    E -->|4. Generate Response| B
    
    B -->|5. Log Tokens & Metadata to Dashboard| F[(Observability DB)]
    B -->|6. Return Response| A
```

## Implementation

Let's look at how to implement these optimizations using the Portkey SDK.

### Step 1: Tagging Requests for Cost Analytics

By passing a `metadata` dictionary during client initialization, every downstream API call is automatically tagged.

```python
!pip install -q portkey-ai

import os
from portkey_ai import Portkey

client = Portkey(
    api_key=os.getenv("PORTKEY_API_KEY"),
    provider="openai",
    Authorization=os.getenv("OPENAI_API_KEY"),
    # Tagging the request enables granular cost dashboards
    metadata={
        "_environment": "production",
        "_user": "tenant_uuid_8472",
        "feature_flag": "invoice_extraction_v2"
    }
)

response = client.chat.completions.create(
    model="gpt-4o",
    messages=[{"role": "user", "content": "Extract data from this invoice..."}]
)
```

In your Portkey dashboard, you can now filter your $500K daily AI spend down to the exact fraction of a cent consumed by `tenant_uuid_8472` using the `invoice_extraction_v2` feature.

### Step 2: Enforcing Budgets

Visibility is step one. Prevention is step two. You can configure budget caps directly in the Portkey UI, or enforce them dynamically via API. If a user tries to generate a massive, recursive loop of tokens, Portkey will sever the connection before OpenAI can bill you.

```python
# Create a budget for a specific user using the Portkey Management SDK
# (Usually executed by your backend when a user signs up)

# A virtual key is bound to a specific provider and budget
virtual_key = client.virtual_keys.create(
    name="tenant_8472_key",
    provider="openai",
    budget={
        "type": "cost",
        "limit": 50.00,        # $50 limit
        "period": "monthly"    # Resets automatically
    }
)

# You then route this specific tenant's traffic using their restricted key,
# guaranteeing they can never cost you more than $50/month.
```

### Step 3: Semantic Caching

The fastest, cheapest LLM request is the one you never make. Portkey provides caching natively at the edge.

```python
# Enable caching with a single config option
cache_config = {
    "cache": {
        "mode": "semantic",  # 'simple' for exact match, 'semantic' for meaning
    }
}

fast_client = client.with_options(config=cache_config)

# Call 1: Reaches OpenAI, takes 2.4 seconds, costs $0.03
response_1 = fast_client.chat.completions.create(
    messages=[{"role": "user", "content": "What is the capital of France?"}]
)

# Call 2 (Different User, Same Intent): Caught by Gateway, takes 15ms, costs $0.00
response_2 = fast_client.chat.completions.create(
    messages=[{"role": "user", "content": "Tell me France's capital city."}]
)
```

## Benchmarks & Results

Implementing these three patterns yields compounding returns. Here is aggregated, anonymized benchmarking data from our top 100 enterprise deployments (representing billions of tokens):

| Optimization Tactic | Implementation Time | Average API Cost Reduction | Average Latency Improvement |
|---------------------|---------------------|----------------------------|-----------------------------|
| Metadata tagging | 5 minutes | 12% (Identifying anomalies) | N/A |
| Budget Caps | 1 day (Backend sync) | 8% (Preventing runaway scripts) | N/A |
| Simple Caching | 2 minutes | 18% | 18% of requests drop to <50ms |
| Semantic Caching | 2 minutes | 34% | 34% of requests drop to <50ms |

By deploying the full suite, our customers typically see a 30-40% reduction in their monthly LLM bills, allowing them to reinvest those savings into scaling their core product.

## Best Practices

1. **Tag Everything**: Never send an untagged request to production. At minimum, append an `_environment` and `_user` tag to every API call.
2. **Start with Simple Caching**: Before enabling vector-based semantic caching, start with simple (exact string match) caching. It has zero computationally overhead and catches identical system prompts.
3. **Use Virtual Keys for Team Budgets**: Don't share raw OpenAI keys among internal development squads. Issue a budget-capped Portkey Virtual Key to the "Marketing GenAI" team and the "Data Pipeline" team separately.

## Conclusion

The era of flying blind with expensive, monolithic LLM APIs is over. With $15M in new funding, Portkey is accelerating the development of the infrastructure layer that makes AI applications financially viable at scale. 

---

## Next Steps

- **Try it yourself**: [Portkey Observability Quickstart](https://portkey.ai/docs/product/observability)
- **Implement Caching**: [Semantic Caching Guide](https://portkey.ai/docs/product/ai-gateway/cache-simple-and-semantic)
- **Explore the gateway**: [GitHub (17K+ Stars)](https://github.com/Portkey-AI/gateway)

---

*Written by Portkey AI, the unified control plane for production LLM apps. Processing over 500B tokens and recognized as a 2025 Gartner Cool Vendor. Follow [@PortkeyAI](https://x.com/PortkeyAI) for more production AI content.*

---

## Metadata

- **Title**: How We Saved Customers Millions After Raising Our $15M Series A
- **Description**: Learn how enterprise engineering teams use Portkey's AI Gateway to track metadata, enforce budget caps, and cache LLM requests to cut API costs by 40%.
- **Tags**: LLM Observability, Cost Optimization, FinOps, Semantic Caching, AI Gateway
- **Estimated read time**: 7 minutes
