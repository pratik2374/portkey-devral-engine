# Never Let Your AI App Go Down: Automatic Fallbacks - Tweet Thread

## Thread

**Tweet 1 (Hook):**
Your AI app just crashed because OpenAI had a 30-minute API outage.

Meanwhile, enterprise apps using an AI Gateway stayed online with literally zero downtime.

Here's how to make your LLM applications bulletproof with automatic fallbacks in 2 minutes:

🧵

**Tweet 2:**
The problem: Most teams build their AI infrastructure with a direct, hardcoded connection to a single provider. 

When that provider goes down—and they all do—your entire application goes completely dark. Customer-facing chatbots break, and internal pipelines halt.

**Tweet 3:**
The fix isn't to write complex error-handling logic around every API call in your codebase. 

The fix is an AI Gateway.

By placing a unified gateway between your app and your LLMs, you can define routing strategies outside of your application logic.

**Tweet 4:**
Step 1: Define a JSON Fallback Strategy.

[screenshot: code-snippet-1]

This config tells the gateway: "Try OpenAI first. If it fails (rate limit, 500 error, timeout), immediately try Anthropic."

**Tweet 5:**
Step 2: Apply the config to your gateway client.

[screenshot: code-snippet-2]

Now, if OpenAI fails, Portkey routes the exact same request body to Claude in under 1ms. 

Portkey even translates the OpenAI-formatted prompt into Anthropic's format automatically. ✨

**Tweet 6:**
The architecture behind this is robust. 
Portkey processes over 500 Billion tokens across 125M daily requests for 24,000+ orgs.

We built this exact fallback routing layer so you don't have to spend weeks maintaining custom, fragile error-handling code.

**Tweet 7:**
What you get for free with Fallbacks:
→ Automatic retries (configurable up to 5x)
→ Cross-provider prompt translation
→ Real-time observability logs showing the exact fallback waterfall

All through a single API.

**Tweet 8:**
Never go down again. Read the full cookbook with working code here:

portkey.ai/docs/product/ai-gateway/fallbacks

⭐ Star the open-source gateway: github.com/Portkey-AI/gateway

Follow @PortkeyAI for more production AI infrastructure tips.

---

## Code Snippets for Screenshots

### code-snippet-1
```python
fallback_config = {
    "strategy": {"mode": "fallback"},
    "targets": [
        {
            "provider": "openai",
            "override_params": {"model": "gpt-4o"}
        },
        {
            "provider": "anthropic",
            "override_params": {"model": "claude-sonnet-4-20250514"}
        }
    ]
}
```

### code-snippet-2
```python
from portkey_ai import Portkey

client = Portkey(api_key="pk-***")
secure_client = client.with_options(config=fallback_config)

# If OpenAI is down, this seamlessly executes via Claude 
# Your users never notice the downtime.
response = secure_client.chat.completions.create(
    messages=[{"role": "user", "content": "Hello!"}]
)
```

---

## Hashtags

#AIGateway #LLM #Portkey #Python #GenAI #ProductionAI #Anthropic #OpenAI #DevOps

---

## Posting Notes

- Best times: 10 AM or 6 PM IST / 9 AM or 1 PM EST
- Tag @OpenAI and @AnthropicAI 
- Reply to first tweet with cookbook link 
- Have a screenshot of the Portkey trace showing a failed OpenAI request triggering a successful Anthropic request in the replies.
