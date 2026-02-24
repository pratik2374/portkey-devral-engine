# AI Gateway Quickstart: Your First Portkey API Call — Sample Cookbook

> **Note**: This is a sample output demonstrating the content engine's cookbook format. In production, this would be generated as a `.ipynb` file.

---

## Cell 1 (Markdown): Title & Overview

# 🚀 AI Gateway Quickstart — Your First Portkey API Call

Route your LLM requests through Portkey's AI Gateway and unlock fallbacks, observability, guardrails, and 250+ model access — all with 2 lines of code.

## What You'll Learn
- Set up the Portkey SDK and make your first API call
- Switch between LLM providers (OpenAI → Anthropic → Google) without changing code
- Add automatic fallbacks for zero-downtime AI apps
- View request logs and costs in the Portkey dashboard

## Prerequisites
- Python 3.9+
- Portkey API Key ([get one free](https://app.portkey.ai))
- OpenAI API key (for first example)

**Time to complete**: ~5 minutes

---

## Cell 2 (Code): Installation

```python
# Install Portkey AI SDK
!pip install -q portkey-ai openai
```

---

## Cell 3 (Code): Setup & Imports

```python
import os
from portkey_ai import Portkey

# Set up API keys
PORTKEY_API_KEY = os.getenv("PORTKEY_API_KEY")
OPENAI_API_KEY = os.getenv("OPENAI_API_KEY")

if not PORTKEY_API_KEY:
    raise ValueError("Please set PORTKEY_API_KEY in your environment variables")

# Initialize Portkey client — routes through the AI Gateway
client = Portkey(
    api_key=PORTKEY_API_KEY,
    provider="openai",
    Authorization=OPENAI_API_KEY
)

print("✅ Portkey client initialized! Requests now route through the AI Gateway.")
```

---

## Cell 4 (Markdown): First API Call

## Step 1: Make Your First Request

Your first request through Portkey's AI Gateway. The API is **fully OpenAI-compatible** — same parameters, same response format, but now with superpowers.

---

## Cell 5 (Code): First API Call

```python
# Your first request through the AI Gateway
response = client.chat.completions.create(
    model="gpt-4o",
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "What is an AI Gateway and why do developers need one?"}
    ],
    max_tokens=200
)

print(response.choices[0].message.content)
print(f"\n📊 Tokens used: {response.usage.total_tokens}")
```

---

## Cell 6 (Markdown): Provider Switching

## Step 2: Switch Providers in One Line

One of Portkey's superpowers — switch between 250+ LLM providers without changing your application code. Just change the `provider` and `Authorization`:

---

## Cell 7 (Code): Provider Switching

```python
# Switch to Anthropic — same API, different provider
anthropic_client = Portkey(
    api_key=PORTKEY_API_KEY,
    provider="anthropic",
    Authorization=os.getenv("ANTHROPIC_API_KEY")
)

response = anthropic_client.chat.completions.create(
    model="claude-sonnet-4-20250514",
    messages=[{"role": "user", "content": "Explain AI Gateways in one sentence."}]
)
print(f"🟣 Anthropic: {response.choices[0].message.content}")

# Switch to Google Gemini
google_client = Portkey(
    api_key=PORTKEY_API_KEY,
    provider="google",
    Authorization=os.getenv("GOOGLE_API_KEY")
)

response = google_client.chat.completions.create(
    model="gemini-2.0-flash",
    messages=[{"role": "user", "content": "Explain AI Gateways in one sentence."}]
)
print(f"🔵 Google: {response.choices[0].message.content}")
```

---

## Cell 8 (Markdown): Fallbacks

## Step 3: Add Automatic Fallbacks

Production AI apps can't depend on a single provider. Add automatic fallbacks so if OpenAI goes down, your app seamlessly switches to Claude:

---

## Cell 9 (Code): Fallbacks

```python
# Fallback config: OpenAI → Anthropic
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

# Apply the fallback config
resilient_client = client.with_options(config=fallback_config)

# This request will try OpenAI first, then Claude if OpenAI fails
response = resilient_client.chat.completions.create(
    messages=[{"role": "user", "content": "Hello from a resilient AI app! 💪"}]
)
print(response.choices[0].message.content)
print("\n✅ Your app now has automatic failover — zero downtime!")
```

---

## Cell 10 (Markdown): Streaming

## Step 4: Streaming Responses

Stream responses for real-time chat experiences:

---

## Cell 11 (Code): Streaming

```python
# Stream a response through the AI Gateway
stream = client.chat.completions.create(
    model="gpt-4o",
    messages=[{"role": "user", "content": "Give me 3 reasons to use an AI Gateway."}],
    stream=True
)

print("🔴 Streaming: ", end="")
for chunk in stream:
    if chunk.choices[0].delta.content:
        print(chunk.choices[0].delta.content, end="", flush=True)
print("\n\n✅ Streaming complete!")
```

---

## Cell 12 (Markdown): Key Takeaways

## 🎯 Key Takeaways

1. **2-Line Integration**: Portkey is OpenAI SDK-compatible — just change the client initialization
2. **Provider Freedom**: Switch between OpenAI, Anthropic, Google, and 250+ providers with one parameter
3. **Automatic Fallbacks**: Add reliability with a config change, not a code rewrite
4. **Full Observability**: Every request is automatically logged in your Portkey dashboard

## Common Gotchas
- Set `PORTKEY_API_KEY` before any provider keys
- Use the `provider` parameter to specify which LLM to route to
- Fallback configs override the provider/model set in the client

---

## Cell 13 (Markdown): Next Steps

## 🚀 Next Steps

- **Add Guardrails**: [Protect your LLM outputs](https://portkey.ai/docs/product/guardrails)
- **Enable Caching**: [Save 30-40% on costs](https://portkey.ai/docs/product/ai-gateway/cache-simple-and-semantic)
- **Monitor Agents**: [Integrate with CrewAI, LangChain](https://portkey.ai/docs/integrations/agents)
- **View Dashboard**: [See your logs and costs](https://app.portkey.ai)

---

⭐ **Star our gateway**: [github.com/Portkey-AI/gateway](https://github.com/Portkey-AI/gateway)

📚 **Full docs**: [portkey.ai/docs](https://portkey.ai/docs/)

🐦 **Follow us**: [@PortkeyAI](https://x.com/PortkeyAI)
