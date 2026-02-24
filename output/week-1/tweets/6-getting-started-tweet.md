# Portkey AI Gateway: Your First API Call in 2 Minutes - Tweet Thread

## Thread

**Tweet 1 (Hook):**
Switching between GPT-4, Claude, and Gemini used to require rewriting your entire codebase to accommodate different SDKs.

Now it takes 1 line of code.

Here's how to route your first request through Portkey's AI Gateway in under two minutes:

🧵

**Tweet 2:**
The problem: Most developers hardcode their AI apps to a single LLM provider (usually OpenAI).

When that provider goes down, or when Claude releases a better/cheaper model, you're stuck. Migrating to a new SDK takes days of engineering effort.

**Tweet 3:**
Step 1: Install Portkey (it's OpenAI-compatible!)

[screenshot: code-snippet-1]

By using the `portkey-ai` Python SDK, you get a clean, familiar interface that routes to 250+ different LLM providers instantly. 

**Tweet 4:**
Step 2: Initialize the client and make a request.

[screenshot: code-snippet-2]

Look familiar? It's the exact same structure as a standard OpenAI call. But now your request is passing through a unified gateway that tracks costs, latency, and tokens automatically. (We handle 125M of these daily).

**Tweet 5:**
Step 3: Switch from OpenAI to Anthropic.

[screenshot: code-snippet-3]

Notice what changed? Just the `provider` string and the API key. 
Zero changes to your prompt structure or array formats. You just migrated providers in seconds without touching your core logic.

**Tweet 6:**
"But my whole massive codebase is already built on the OpenAI SDK!"

No problem. You don't have to rewrite anything. You can route the standard, raw OpenAI SDK through Portkey by changing just 2 lines of initialization code:

[screenshot: code-snippet-4]

**Tweet 7:**
What you get for free on every request:
→ Zero-code provider switching
→ Deep observability & cost tracking dashboards
→ Access to 250+ models (including Claude Haiku 4.5 & Gemini 1.5)

Plus, you can add Fallbacks and Retries later with one config change.

**Tweet 8:**
Read the full quickstart cookbook and get your first request running today:

https://portkey.ai/docs/welcome/make-your-first-request

⭐ Star the open-source gateway: github.com/Portkey-AI/gateway

Follow @PortkeyAI for more production AI infrastructure tips.

---

## Code Snippets for Screenshots

### code-snippet-1
```bash
pip install portkey-ai
```

### code-snippet-2
```python
import os
from portkey_ai import Portkey

# Initialize Portkey client
client = Portkey(
    api_key=os.getenv("PORTKEY_API_KEY"),
    provider="openai",
    Authorization=os.getenv("OPENAI_API_KEY")
)

response = client.chat.completions.create(
    model="gpt-4o",
    messages=[{"role": "user", "content": "Hello!"}]
)
```

### code-snippet-3
```python
import os
from portkey_ai import Portkey

# Switch to Anthropic — just change provider and auth
anthropic_client = Portkey(
    api_key=os.getenv("PORTKEY_API_KEY"),
    provider="anthropic",
    Authorization=os.getenv("ANTHROPIC_API_KEY")
)

response = anthropic_client.chat.completions.create(
    model="claude-3-5-sonnet-20241022",
    messages=[{"role": "user", "content": "Hello via Anthropic!"}]
)
```

### code-snippet-4
```python
from openai import OpenAI
from portkey_ai import PORTKEY_GATEWAY_URL, createHeaders

# Standard OpenAI SDK routed through Portkey
client = OpenAI(
    api_key=os.getenv("OPENAI_API_KEY"),
    base_url=PORTKEY_GATEWAY_URL,           # ← Line 1
    default_headers=createHeaders(           # ← Line 2
        api_key=os.getenv("PORTKEY_API_KEY"),
        provider="openai"
    )
)
```

---

## Hashtags

#AIGateway #LLM #Portkey #Python #GenAI #ProductionAI #OpenAI #Anthropic

---

## Posting Notes

- Best times: 10 AM or 6 PM IST / 9 AM or 1 PM EST
- Tag @OpenAI and @AnthropicAI when discussing specific providers
- Reply to first tweet with cookbook link if needed
- Engage with replies for first 30 mins
