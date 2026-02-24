# Cookbook Template (Jupyter Notebook)

Use this structure when generating Jupyter notebook cookbooks (`.ipynb` files) for Portkey AI.

---

## Notebook Structure

```json
{
  "cells": [
    // Cell 1: Title & Overview (Markdown)
    // Cell 2: Prerequisites & Installation (Markdown + Code)
    // Cell 3: Setup & Imports (Code)
    // Cell 4-N: Implementation with explanations
    // Cell N+1: Provider Switching Demo (Code)
    // Cell N+2: Key Takeaways (Markdown)
    // Cell N+3: Next Steps & CTA (Markdown)
  ]
}
```

---

## Cell 1: Title & Overview

```markdown
# [Title] — Portkey AI Cookbook

[1-2 sentence hook — why this matters for production AI apps]

## What You'll Learn
- [Outcome 1 — e.g., "Route requests across multiple LLM providers"]
- [Outcome 2 — e.g., "Add automatic fallbacks for 99.9% uptime"]
- [Outcome 3 — e.g., "Separate prompts from code using the Prompt Library"]
- [Outcome 4 — e.g., "Monitor costs, latency, and custom metadata in real-time"]

## Prerequisites
- Python 3.9+
- Portkey API Key ([get one free](https://app.portkey.ai))
- At least one LLM provider API key (OpenAI, Anthropic, etc.)

**Time to complete**: ~[X] minutes
```

---

## Cell 2: Installation

```python
# Install Portkey AI SDK
!pip install -q portkey-ai openai
```

---

## Cell 3: Setup & Imports

```python
import os
from portkey_ai import Portkey

# Load API keys
PORTKEY_API_KEY = os.getenv("PORTKEY_API_KEY")
OPENAI_API_KEY = os.getenv("OPENAI_API_KEY")

if not PORTKEY_API_KEY:
    raise ValueError("Please set PORTKEY_API_KEY in your environment variables")

# Initialize Portkey client
client = Portkey(
    api_key=PORTKEY_API_KEY,
    provider="openai",
    Authorization=OPENAI_API_KEY
)

print("✅ Portkey client initialized!")
```

---

## Cell 4-N: Implementation

Each implementation section follows this pattern:

**Markdown cell before code:**
```markdown
## [Step N]: [What we're doing]

[1-2 sentences explaining WHY this step matters for production AI]
```

**Code cell:**
```python
# [Brief comment about what this does]
response = client.chat.completions.create(
    model="gpt-4o",
    messages=[{"role": "user", "content": "Hello from Portkey!"}]
)
print(response.choices[0].message.content)
```

---

## Provider Switching Demo Cell

Every cookbook should include a provider switching demo:

```markdown
## 🔄 Switch Providers in One Line

One of Portkey's superpowers — switch between 250+ LLM providers without changing your code:
```

```python
# Switch to Anthropic — just change provider and auth
anthropic_client = Portkey(
    api_key=PORTKEY_API_KEY,
    provider="anthropic",
    Authorization=os.getenv("ANTHROPIC_API_KEY")
)

response = anthropic_client.chat.completions.create(
    model="claude-sonnet-4-20250514",
    messages=[{"role": "user", "content": "Hello from Portkey via Anthropic!"}]
)
print(f"Anthropic says: {response.choices[0].message.content}")
```

---

## Key Takeaways Cell (Markdown)

```markdown
## 🎯 Key Takeaways

1. **[Takeaway 1]**: [e.g., "Portkey acts as a unified gateway to all your LLM providers"]
2. **[Takeaway 2]**: [e.g., "Adding fallbacks takes just a config change, not a code rewrite"]
3. **[Takeaway 3]**: [e.g., "Every request is automatically logged for observability"]

## Common Gotchas
- Always set `PORTKEY_API_KEY` before provider keys
- Use `provider` parameter to specify which LLM provider to route to
- Configs can be created in the Portkey dashboard or inline in code
```

---

## Next Steps Cell (Markdown)

```markdown
## 🚀 Next Steps

- **Add Guardrails**: [Protect your LLM outputs](https://portkey.ai/docs/product/guardrails)
- **Enable Caching**: [Reduce costs with semantic caching](https://portkey.ai/docs/product/ai-gateway/cache-simple-and-semantic)
- **Manage Prompts**: [Iterate rapidly with Prompt Library](https://portkey.ai/docs/product/prompt-library)
- **Monitor in Dashboard**: [Analyze logs with custom metadata](https://portkey.ai/docs/product/observability)

---

⭐ **Star our gateway**: [github.com/Portkey-AI/gateway](https://github.com/Portkey-AI/gateway)

📚 **Full docs**: [portkey.ai/docs](https://portkey.ai/docs/)

🐦 **Follow us**: [@PortkeyAI](https://x.com/PortkeyAI)
```

---

## Code Style Guidelines

1. **Use `portkey_ai` SDK** as the primary interface
2. **Show OpenAI compatibility** where relevant (2-line migration)
3. **Clear variable names**: `client` not `c`, `response` not `r`
4. **Helpful comments**: Explain the "why" not the "what"
5. **Error handling**: Wrap API calls in try/except
6. **Progress indicators**: Use print statements with emojis
7. **Clean output**: Format results nicely

---

## Error Handling Pattern

```python
try:
    response = client.chat.completions.create(
        model="gpt-4o",
        messages=[{"role": "user", "content": prompt}]
    )
    result = response.choices[0].message.content
    print(f"✅ Response: {result}")
except Exception as e:
    print(f"❌ Error: {e}")
    print("💡 Tips:")
    print("  - Check your PORTKEY_API_KEY is valid")
    print("  - Verify your provider API key is set")
    print("  - Ensure the model name is correct")
    raise
```

---

## File Naming

Format: `{bucket}-{short-title}.ipynb`

Examples:
- `gateway-quickstart-fallbacks.ipynb`
- `observability-cost-tracking.ipynb`
- `agents-crewai-with-portkey.ipynb`
- `getting-started-first-api-call.ipynb`
