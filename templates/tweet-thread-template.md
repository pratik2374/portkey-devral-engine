# Tweet Thread Template

Use this structure when generating tweet threads (`.md` files in `tweets/` folder) for Portkey AI.

---

## File Structure

```markdown
# [Title] - Tweet Thread

## Thread

**Tweet 1 (Hook):**
[content]

**Tweet 2:**
[content]

...

**Tweet N (CTA):**
[content]

---

## Code Snippets for Screenshots

[Code blocks formatted for visual screenshots]

---

## Hashtags

[Relevant hashtags]

---

## Posting Notes

[Timing, tagging, engagement strategy]
```

---

## Hook Formulas (Tweet 1)

Use one of these proven patterns:

### Pattern 1: Production Pain Point
```
Your AI app just went down because OpenAI had an outage.

Here's how to make it bulletproof with 2 lines of code:

🧵
```

### Pattern 2: Cost Savings
```
We saved $[X]K/month on LLM costs with one config change.

Here's exactly how (with code):

🧵
```

### Pattern 3: Simplification
```
Switching between GPT-4, Claude, and Gemini used to require rewriting your entire codebase.

Now it takes 1 line:

🧵
```

### Pattern 4: Feature Announcement
```
Portkey just shipped [feature].

Here's what it means for your AI apps:

🧵
```

### Pattern 5: Comparison / Benchmark
```
I routed 1M requests through [X] AI providers.

Here's what happened to latency, costs, and reliability:

🧵
```

### Pattern 6: Prompt Versioning
```
Stop checking prompts into git.

Every time you tweak a system prompt, you're waiting on a full PR and deployment cycle. 

There's a better way:

🧵
```

---

## Thread Structure (5-8 tweets)

### Tweet 1: Hook
- Stop the scroll with a production AI pain point
- Create curiosity about the solution
- Max 200 chars to leave room for engagement

### Tweet 2: Problem / Context
- Why this matters for developers building with LLMs
- Relatable pain point (cost, reliability, vendor lock-in)

### Tweet 3-5: Solution with Code
- Show Portkey code snippets (describe for screenshots)
- One concept per tweet
- Emphasize the simplicity (2-line integration)

### Tweet 6: Results / Benefits
- What you achieve (uptime, cost savings, flexibility)
- Benchmarks if applicable

### Tweet 7: CTA
- Link to Portkey docs or cookbook
- Encourage GitHub star
- Ask for follow

---

## Code Snippet Guidelines

Code snippets for screenshots should be:

1. **5-12 lines**: Fits nicely in image
2. **Self-contained**: Makes sense without context
3. **Show `portkey_ai` import**: Brand recognition
4. **Clean formatting**: No long lines, proper indentation

### Good Example:
```python
from portkey_ai import Portkey

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

### Fallback Example (great for engagement):
```python
config = {
    "strategy": {"mode": "fallback"},
    "targets": [
        {"provider": "openai", "override_params": {"model": "gpt-4o"}},
        {"provider": "anthropic", "override_params": {"model": "claude-sonnet-4-20250514"}}
    ]
}

client = client.with_options(config=config)
# If OpenAI fails → auto-switches to Claude ✨
```

### Prompt Management Example:
```python
# Execute a versioned prompt from the cloud
response = client.prompts.completions.create(
    prompt_id="pp-marketing-copy-v2",
    variables={
        "product_name": "Portkey",
        "tone": "excited"
    }
)
# No more prompt strings in your codebase ✨
```

---

## Sample Complete Thread

```markdown
# AI Gateway Fallbacks - Tweet Thread

## Thread

**Tweet 1 (Hook):**
Your AI app crashed because OpenAI had a 30-minute outage.

Meanwhile, apps using an AI Gateway stayed up with zero downtime.

Here's how to add automatic fallbacks in 2 minutes:

🧵

**Tweet 2:**
The problem: Most apps hardcode a single LLM provider.

When that provider goes down, your entire app goes down.

The fix? An AI Gateway that auto-routes to backup providers.

**Tweet 3:**
Step 1: Install Portkey (it's OpenAI-compatible)

[screenshot: code-snippet-1]

That's it. Your existing OpenAI code works unchanged.

**Tweet 4:**
Step 2: Add a fallback config

[screenshot: code-snippet-2]

Now if GPT-4 fails → it auto-switches to Claude.
Zero code changes. Zero downtime.

**Tweet 5:**
What you get for free:
→ Automatic retries (up to 5x)
→ Load balancing across providers
→ Real-time logs & cost tracking
→ 50+ guardrails for safety

All through a single unified API.

**Tweet 6:**
Full cookbook with working code:

portkey.ai/docs

⭐ Star the gateway: github.com/Portkey-AI/gateway

Follow @PortkeyAI for more production AI tips.

---

## Code Snippets for Screenshots

### code-snippet-1
```python
from portkey_ai import Portkey

# Drop-in replacement for OpenAI
client = Portkey(
    api_key="pk-***",
    provider="openai",
    Authorization="sk-***"
)

# Same API, but now with superpowers
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
client = client.with_options(config=config)
```

---

## Hashtags

#AIGateway #LLM #Portkey #Python #GenAI #ProductionAI

---

## Posting Notes

- Best times: 10 AM or 6 PM IST / 9 AM or 1 PM EST
- Tag relevant people when discussing specific providers
- Reply to first tweet with cookbook link if needed
- Engage with replies for first 30 mins
```

---

## File Naming

Format: `{bucket}-{short-title}-tweet.md`

Examples:
- `gateway-fallbacks-tweet.md`
- `observability-cost-tracking-tweet.md`
- `agents-crewai-integration-tweet.md`
- `getting-started-quickstart-tweet.md`
