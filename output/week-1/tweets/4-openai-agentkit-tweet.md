# Run OpenAI AgentKit Through Portkey's AI Gateway - Tweet Thread

## Thread

**Tweet 1 (Hook):**
OpenAI Swarm/AgentKit is incredible, but putting autonomous agents in production is terrifying.

They can burn through API credits, hallucinate tool calls, and create infinite loops.

Here is how to monitor your agents and cap their budgets with a 2-line code change:

🧵

**Tweet 2:**
The problem: Autonomous agents make dozens of LLM calls in a loop. 

When an agent fails in production, looking at raw API logs is useless. You need to see the "waterfall"—the exact sequence of thoughts, tool executions, and LLM responses grouped together in one trace.

**Tweet 3:**
Step 1: Upgrade the Swarm Client.
Swarm uses the standard OpenAI python client. You can route that client through Portkey's AI Gateway by changing just two lines:

[screenshot: code-snippet-1]

By adding a `trace_id`, Portkey automatically groups every loop iteration together.

**Tweet 4:**
Wait, does it only work with OpenAI models?
No.
Because Portkey sits between the SDK and the provider, it translates payloads automatically.

You can run OpenAI Swarm on Anthropic's Claude Haiku 4.5. Just change the provider string!

[screenshot: code-snippet-2]

**Tweet 5:**
What happens when you route agents through Portkey?
1. Visual Waterfall Tracing: See the exact handoffs between Triage Agents and Support Agents.
2. Structured Tool Calls: Instantly see if the agent hallucinated a JSON parameter.
3. Cost Analytics: Track exactly how much each agent is spending.

**Tweet 6:**
Budget Caps for Agents.
Terrified your agent will get stuck in a loop and rack up a $10,000 bill overnight?

Portkey Virtual Keys allow you to set strict budget caps. "Block this agent if it spends more than $10 today." The gateway cuts off the API immediately.

**Tweet 7:**
Portkey processes over 500B tokens across 125M daily requests. We built this tracing infrastructure specifically so you don't have to build custom dashboards for your agentic workflows.

**Tweet 8:**
Check out the fully running Jupyter Cookbook to route your first AgentKit workflow through Portkey today:

portkey.ai/docs/integrations/agents/openai-swarm

⭐ Star the open-source gateway: github.com/Portkey-AI/gateway

Follow @PortkeyAI for more production AI infrastructure tips.

---

## Code Snippets for Screenshots

### code-snippet-1
```python
from openai import OpenAI
from swarm import Swarm
from portkey_ai import PORTKEY_GATEWAY_URL, createHeaders

# Route Swarm through Portkey for tracing & observability
portkey_client = OpenAI(
    base_url=PORTKEY_GATEWAY_URL,
    default_headers=createHeaders(
        api_key=PORTKEY_API_KEY,
        provider="openai",
        trace_id="multi_agent_support_ticket_1092" # Groups the trace!
    )
)

swarm_client = Swarm(client=portkey_client)
```

### code-snippet-2
```python
# Run OpenAI Swarm on Claude!
anthropic_client = OpenAI(
    base_url=PORTKEY_GATEWAY_URL,
    default_headers=createHeaders(
        api_key=PORTKEY_API_KEY,
        provider="anthropic", # Portkey translates the payload!
    )
)

claude_swarm = Swarm(client=anthropic_client)
```

---

## Hashtags

#AIGateway #LLM #Portkey #Python #GenAI #AgenticAI #OpenAI #AgentKit #Observability

---

## Posting Notes

- Best times: 10 AM or 6 PM IST / 9 AM or 1 PM EST
- Tag @OpenAI 
- Include a beautiful screenshot of the Portkey Waterfall Trace UI in the replies.
