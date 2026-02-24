# Enterprise-Grade Protection: Portkey x Javelin AI Security - Tweet Thread

## Thread

**Tweet 1 (Hook):**
One simple "Ignore previous instructions" prompt can force your enterprise AI chatbot to leak your internal data or curse at your customers.

Deploying LLMs without security pipelines is a massive liability.

Here's how to secure them with military-grade Guardrails in 2 minutes:

🧵

**Tweet 2:**
The problem: Rule-based regex blockers don't work against sophisticated jailbreaks like the 'DAN' (Do Anything Now) prompt. 

You need advanced, AI-native security scanners to mathematically evaluate user inputs before they ever reach OpenAI or Anthropic.

**Tweet 3:**
Step 1: Define an Input Guardrail Pipeline.

[screenshot: code-snippet-1]

Portkey integrates natively with Javelin AI Security. You just add their API key and configure the `prompt_injection` threshold. 

If a user tries a malicious jailbreak, Portkey blocks the request instantly.

**Tweet 4:**
Step 2: Add Output Guardrails.

[screenshot: code-snippet-2]

What if the LLM hallucinates and accidentally generates an email address, a social security number (PII), or highly toxic language? 

The Output Guardrail intercepts the generation before it reaches the user and denies it.

**Tweet 5:**
Step 3: Combine with Automatic Retries.

If the LLM generates something that triggers an output block, you don't necessarily want to send an error to your user.

Combine Guardrails with Retries! Portkey will silently retry the prompt up to 5 times to generate a safe response.

**Tweet 6:**
When you manage 125M daily requests like Portkey does, security can't be an afterthought scattered across your application code. 

It must be declarative, infrastructure-level API routing. 

**Tweet 7:**
Our unified control plane features 50+ pre-built guardrails—from PII redaction and language detection to JSON validation.

This is exactly why we were heavily vetted and awarded the 2025 Gartner® Cool Vendor™ recognition for LLM Observability & Governance.

**Tweet 8:**
Check out the fully functional Python Cookbook to secure your AI apps against prompt injections today:

portkey.ai/docs/product/guardrails

⭐ Star the open-source gateway: github.com/Portkey-AI/gateway

Follow @PortkeyAI for more production AI infrastructure tips.

---

## Code Snippets for Screenshots

### code-snippet-1
```python
from portkey_ai import Portkey

client = Portkey(api_key="pk-***")

# Configure Javelin AI's military-grade prompt injection detection
guardrail_config = {
    "input_guardrails": [
        {
            "provider": "javelin",
            "api_key": "javelin-***",
            # Block the request if it looks like a jailbreak
            "javelin.prompt_injection": {"threshold": 0.8},
            "deny": True
        }
    ]
}
```

### code-snippet-2
```python
# Add Output Guards for PII & Toxicity
comprehensive_config = {
    **guardrail_config, # Include the input guard
    "output_guardrails": [
        {
            "provider": "javelin",
            "api_key": "javelin-***",
            "javelin.pii": {"threshold": 0.9},        # Block SSNs
            "javelin.toxicity": {"threshold": 0.75},   # Block harmful language
            "deny": True
        }
    ],
    # Automatically retry the LLM if an output guard trips!
    "retry": {"attempts": 3}
}

secure_client = client.with_options(config=comprehensive_config)
```

---

## Hashtags

#AIGateway #LLM #Portkey #Python #GenAI #CyberSecurity #PromptInjection #Infosec #DevSecOps

---

## Posting Notes

- Best times: 10 AM or 6 PM IST / 9 AM or 1 PM EST
- Tag @JavelinAI (or relevant Javelin handles)
- Mention Gartner Cool Vendor recognition to boost authority 
