# Monitor Your CrewAI Agents with Portkey - Tweet Thread

## Thread

**Tweet 1 (Hook):**
Running a multi-agent CrewAI system in production? 

If you aren't tracking exactly how many tokens your "Researcher" agent consumes vs your "Writer" agent, your API costs are going to spiral out of control.

Here's how to trace every agent automatically:

🧵

**Tweet 2:**
The problem: CrewAI is powerful, but it abstracts away the underlying API calls. 

When your script takes 45 seconds to run, you have no idea if it's because OpenAI is slow today, or if your "Reviewer" agent got stuck in a recursive loop parsing a large document.

**Tweet 3:**
You need Agent-Level Observability.
You need to see a visual waterfall of every LLM interaction, every tool execution, and the exact cost of every single step.

This takes 1 line of configuration using Portkey's AI Gateway.

**Tweet 4:**
Step 1: Use Portkey as the LLM backend for CrewAI.

[screenshot: code-snippet-1]

Portkey integrates natively with LangChain (which powers CrewAI). You simply pass the Portkey LLM instance to your agents. 

**Tweet 5:**
By passing a `trace_id` alongside custom metadata like `agent_name`, Portkey structures the chaotic asynchronous calls of your multi-agent system into cleanly organized logs.

[screenshot: code-snippet-2]

**Tweet 6:**
What you get in the Portkey Dashboard:
→ Agent A vs Agent B cost breakdowns
→ Exact timestamps for every tool execution
→ Fallback routing (If OpenAI fails, the Crew automatically switches to Claude without throwing an error)

**Tweet 7:**
We handle 125M daily requests, and we see the most advanced teams deploying autonomous systems. The one thing they all have in common? They never let agents touch an LLM API directly without a gateway layer in between.

**Tweet 8:**
Get full visibility into your CrewAI squads. Read the integration guide here:

portkey.ai/docs/integrations/agents/crewai

⭐ Star the open-source gateway: github.com/Portkey-AI/gateway

Follow @PortkeyAI for more production AI infrastructure tips.

---

## Code Snippets for Screenshots

### code-snippet-1
```python
from langchain_community.chat_models import ChatPortkey
from crewai import Agent, Task, Crew

# Initialize Portkey as the LLM backend
portkey_llm = ChatPortkey(
    api_key="pk-***",
    provider="openai",
    model="gpt-4o",
    trace_id="crewai_research_run_101"
)
```

### code-snippet-2
```python
# Pass the Portkey LLM to your agents
researcher = Agent(
    role='Senior Research Analyst',
    goal='Uncover AI trends in 2026',
    backstory='You are an expert analyst.',
    llm=portkey_llm
)

# Every thought and action is now traced, timed, 
# and cost-calculated in your Portkey dashboard!
```

---

## Hashtags

#AIGateway #LLM #Portkey #Python #GenAI #CrewAI #Agents #Observability

---

## Posting Notes

- Best times: 10 AM or 6 PM IST / 9 AM or 1 PM EST
- Tag @crewaiInc 
- Include a screenshot of the Portkey trace dashboard in the replies showing agent separation.
