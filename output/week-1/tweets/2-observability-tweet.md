# Why We Were Named a 2025 Gartner Cool Vendor in LLM Observability - Tweet Thread

## Thread

**Tweet 1 (Hook):**
Are you flying blind with your LLM usage in production?

If you can't tell which specific user generated which API cost, or exactly why an AI agent hallucinated a tool call, you have a massive visibility problem.

Here's how to fix it in 3 lines of code:

🧵

**Tweet 2:**
The problem: AI traffic isn't like normal HTTP traffic. 
It contains complex nested json (tools, arrays, embeddings). Standard DevOps tools like Datadog don't understand it out-of-the-box. 

When an LLM outputs malformed JSON in production, debugging raw text logs is a nightmare.

**Tweet 3:**
This is why Portkey was just recognized as a 2025 Gartner® Cool Vendor™ in AI Observability.

Our AI Gateway natively understands the unique payloads of 250+ LLMs and structures them for deep analytics.

We currently process over 500 Billion tokens, providing X-ray vision for 24,000+ teams.

**Tweet 4:**
Step 1: Tag your requests with Metadata.

[screenshot: code-snippet-1]

By appending a custom `_user` or `environment` tag, Portkey automatically segments all your API costs, latency, and tokens in a beautiful graphical dashboard.

**Tweet 5:**
Step 2: Group Multi-Step Agent Workflows.

[screenshot: code-snippet-2]

Building an Agent with LangChain or CrewAI? Attach a `trace_id` to your client. 

Portkey will group all the discrete LLM calls the agent makes into a single, visual "waterfall" trace. You see exactly what the agent was thinking.

**Tweet 6:**
Step 3: Analyze Tool Calls.

Because Portkey understands native LLM structures, our dashboards specifically highlight Function/Tool interactions.
You instantly see if a failing workflow is due to the LLM hallucinating a parameter type, or your API timing out.

**Tweet 7:**
What you get:
→ Real-time cost & latency dashboards
→ Searchable request logs stored securely
→ Export capability via OpenTelemetry to your existing monitoring stack

All without slowing down your requests by a single millisecond.

**Tweet 8:**
Read the full cookbook and start monitoring your production AI apps the right way:

portkey.ai/docs/product/observability

⭐ Star the open-source gateway: github.com/Portkey-AI/gateway

Follow @PortkeyAI for more production AI infrastructure tips.

---

## Code Snippets for Screenshots

### code-snippet-1
```python
from portkey_ai import Portkey

client = Portkey(
    api_key="pk-***",
    provider="openai",
    Authorization="sk-***",
    # Tag requests to segment your dashboard analytics!
    metadata={
        "_environment": "production",
        "_user": "tenant_uuid_1092",
        "feature": "invoice_extraction"
    }
)

response = client.chat.completions.create(
    model="gpt-4o",
    messages=[{"role": "user", "content": "Extract data..."}]
)
```

### code-snippet-2
```python
# Trace complex agentic workflows
client = client.with_options(
    # Groups multiple API calls into a single visual span
    trace_id="document_processing_agent_run_49" 
)

# Step 1: Agent plans
res1 = client.chat.completions.create(...)

# Step 2: Agent executes tool
res2 = client.chat.completions.create(...)

# Both calls are linked in your Portkey dashboard automatically!
```

---

## Hashtags

#AIGateway #LLM #Portkey #Python #GenAI #ProductionAI #Observability #Gartner

---

## Posting Notes

- Best times: 10 AM or 6 PM IST / 9 AM or 1 PM EST
- Mention Gartner's Cool Vendor recognition to boost authority 
- Have a screenshot of the Portkey Observability Dashboard in the replies.
