# Load Balancing LLM Requests Across API Keys - Tweet Thread

## Thread

**Tweet 1 (Hook):**
Your AI app just hit OpenAI's 10,000 requests-per-minute rate limit. 

Your users are getting 429 Too Many Requests errors. You're losing money and trust.

Here's how to multiply your rate limits instantly by load balancing across multiple API keys:

🧵

**Tweet 2:**
The problem: Every LLM provider enforces strict rate limits per account/API key. 

If your application scales rapidly or triggers a massive batch-processing job, you will hit these ceilings. Upgrading your tier can take days of manual approval from the provider.

**Tweet 3:**
The fix? 

Take 3 different OpenAI API keys (from different accounts or tiers) and distribute your traffic evenly across them. 

Instead of waiting for OpenAI to manually raise your limit, you just tripled it yourself.

**Tweet 4:**
Step 1: Set up a Load Balancing configuration.

[screenshot: code-snippet-1]

With Portkey's Gateway, you simply define the targets. Here, we're splitting traffic exactly 50/50 between two different OpenAI API keys by assigning them equal weights.

**Tweet 5:**
Step 2: Start routing your requests. 

[screenshot: code-snippet-2]

Your application code never changes. Portkey transparently handles the request distribution behind the scenes. 
If Key 1 hits its rate limit, Portkey's gateway will seamlessly route the traffic to Key 2.

**Tweet 6:**
You can also optimize for cost, not just rate limits. 

Have an expensive Azure OpenAI deployment and a cheaper direct OpenAI account? 
Set custom weights! Route 80% to the cheap account, and 20% to the enterprise account.

**Tweet 7:**
What you get:
→ Instant rate limit multiplication 
→ Multi-tenant cost optimization 
→ Real-time observability to see exactly which keys are absorbing the traffic

All managed through a unified API that handles 125M+ requests every day.

**Tweet 8:**
Never hit a 429 error again. 

Learn how to configure intelligent Load Balancing in our official docs:
portkey.ai/docs/product/ai-gateway/load-balancing

⭐ Star the open-source gateway: github.com/Portkey-AI/gateway

Follow @PortkeyAI for more GenAI architecture tips.

---

## Code Snippets for Screenshots

### code-snippet-1
```python
lb_config = {
    "strategy": {"mode": "loadbalance"},
    "targets": [
        {
            "provider": "openai",
            "api_key": OPENAI_KEY_1,
            "weight": 1  # 50% of traffic
        },
        {
            "provider": "openai",
            "api_key": OPENAI_KEY_2,
            "weight": 1  # 50% of traffic
        }
    ]
}
```

### code-snippet-2
```python
from portkey_ai import Portkey

# Initialize with the load-balancing configuration
client = Portkey(api_key="pk-***").with_options(config=lb_config)

# Send your requests! Traffic will be split automatically.
# Your code doesn't need to know which key is being used.
response = client.chat.completions.create(
    messages=[{"role": "user", "content": "Extract data..."}]
)
```

---

## Hashtags

#AIGateway #LLM #Portkey #Python #GenAI #ProductionAI #OpenAI #RateLimits

---

## Posting Notes

- Best times: 10 AM or 6 PM IST / 9 AM or 1 PM EST
- Tag @OpenAI 
- Reply to first tweet with documentation link 
- Have a screenshot of the Portkey trace showing a 429 error seamlessly routed to a healthy key in the replies.
