# AI Gateway Quickstart - Tweet Thread

## Thread

**Tweet 1 (Hook):**
Your OpenAI API key costs you $500/month.

With 2 lines of code, you can add fallbacks, caching, and cut that by 40%.

Here's how:

🧵

**Tweet 2:**
The problem: Most AI apps hardcode one LLM provider.

When it goes down → your app goes down.
When prices increase → you eat the cost.
When you want to try Claude → you rewrite everything.

There's a better way.

**Tweet 3:**
Meet the AI Gateway pattern.

One API that routes to 250+ LLMs:

[screenshot: code-snippet-1]

Same OpenAI-compatible API. But now your requests flow through an intelligent gateway.

**Tweet 4:**
The magic? Automatic fallbacks.

If GPT-4 fails → it switches to Claude instantly:

[screenshot: code-snippet-2]

Zero code changes. Zero downtime. Just a config.

**Tweet 5:**
But wait — there's more you get for free:

→ 📊 Real-time logs & cost tracking
→ 🛡️ 50+ guardrails for output safety
→ ⚡ Semantic caching (save 30-40%)
→ ⚖️ Load balancing across API keys
→ 🔄 Automatic retries with backoff

All through ONE unified API.

**Tweet 6:**
The best part? If you already use the OpenAI SDK, it's a 2-line change:

[screenshot: code-snippet-3]

Everything else in your code stays exactly the same.

**Tweet 7 (CTA):**
Full quickstart guide:
portkey.ai/docs/introduction/make-your-first-request

Open-source gateway (17K+ ⭐):
github.com/Portkey-AI/gateway

Follow @PortkeyAI for more production AI tips.

---

## Code Snippets for Screenshots

### code-snippet-1
```python
from portkey_ai import Portkey

# Route through the AI Gateway
client = Portkey(
    api_key="pk-***",
    provider="openai",
    Authorization="sk-***"
)

response = client.chat.completions.create(
    model="gpt-4o",
    messages=[{"role": "user", "content": "Hello!"}]
)
```

### code-snippet-2
```python
config = {
    "strategy": {"mode": "fallback"},
    "targets": [
        {"provider": "openai",
         "override_params": {"model": "gpt-4o"}},
        {"provider": "anthropic",
         "override_params": {"model": "claude-sonnet-4-20250514"}}
    ]
}
# If OpenAI fails → auto-switches to Claude ✨
client = client.with_options(config=config)
```

### code-snippet-3
```python
from openai import OpenAI
from portkey_ai import PORTKEY_GATEWAY_URL, createHeaders

client = OpenAI(
    api_key="sk-***",
    base_url=PORTKEY_GATEWAY_URL,          # ← Line 1
    default_headers=createHeaders(          # ← Line 2
        api_key="pk-***",
        provider="openai"
    )
)
# Everything else stays the same!
```

---

## Hashtags

#AIGateway #LLM #Portkey #Python #GenAI #ProductionAI #OpenAI

---

## Posting Notes

- Best times: 10 AM IST / 9 AM EST (Tuesday or Wednesday)
- Tag @OpenAI and @AnthropicAI when mentioning their models
- Reply to first tweet with link to cookbook if it doesn't fit
- Engage with replies for first 30 minutes
- Pin this thread if it gets good engagement
