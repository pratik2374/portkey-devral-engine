# SKILL: Viral Tweet Generator

## Trigger
Use this skill when a user asks to:
- Write a tweet, thread, or X post
- Generate viral social media content
- Create a tweet about a topic, tool, news, or idea
- Turn a content idea into a tweet
- Repurpose content as a tweet
- Save a tweet thread as a `.md` file

---

## Step 1: Gather Context

Before generating, identify:

1. **Topic / Content Idea** — What is the tweet about? (tool, news, insight, result, opinion, code demo)
2. **Output Type** — Single tweet OR full thread (default to thread if topic is educational/technical)
3. **Format** — Which viral format fits best? (see Format Menu below)
4. **Tone** — Technical & Expert / Casual & Relatable / Bold & Provocative / Educational
5. **Code Snippet?** — If the topic involves a tool or workflow, include a code example formatted for screenshot
6. **Web Search Needed?** — If the topic is a recent AI tool, news event, launch, or trend, use web search BEFORE writing

If the user hasn't specified format or tone, **infer from the topic** and pick the best fit. Do not ask multiple clarifying questions — make a smart default and proceed.

---

## Step 2: Web Search (When Needed)

Use web search when the topic involves:
- A recently released AI tool, model, or framework
- A conference, launch event, or announcement
- Current statistics, benchmarks, or metrics
- Any claim where recency adds credibility

Search query examples:
- `"[tool name] launch features 2026"`
- `"[AI model] benchmark latency cost"`
- `"[company] AI announcement February 2026"`

Extract: specific numbers, dates, feature names, notable comparisons — these make tweets credible and shareable.

---

## Step 3: Select Format

### Single Tweet vs. Thread Decision
- **Single tweet** → Opinion, hot take, quick tip, before/after, result stat
- **Thread (5–8 tweets)** → Technical tutorial, tool launch, comparison, how-I story, list post

### FORMAT MENU

| Format | Best For | Viral Trigger | Type |
|--------|----------|---------------|------|
| **Top X List** | News, tool launches, events | Curiosity gap + scannability | Thread |
| **Comparison** | Two competing tools/models | Saves audience time + "shocked me" | Thread |
| **How I Did It** | Personal workflow, results | Authority + aspiration | Thread |
| **Tutorial / Code Walk** | Technical education | Step-by-step value | Thread |
| **Production Pain Point** | Reliability, cost, outages | Immediate relatability | Thread |
| **Quick Tip** | Productivity hack, prompt trick | Instant value | Single |
| **Hot Take** | Contrarian opinion | Debate + shareability | Single |
| **Prediction** | Trends, future of AI | Stakes a position | Single |
| **Results/Proof** | Metrics, build-in-public | Credibility + FOMO | Single/Thread |
| **Mistake Story** | Lessons learned | Vulnerability + trust | Single/Thread |
| **Before/After** | Time saved, transformation | Concrete proof | Single |
| **Feature Announcement** | New product/tool capability | FOMO + news value | Thread |

---

## Step 4: Write the Content

### Universal Rules (Apply to Every Tweet)

1. **Line 1 = scroll stopper.** Specific, surprising, or bold. Never start with "I think" or vague statements.
2. **Use specific numbers.** Not "faster" → "3x faster". Not "many tools" → "7 tools".
3. **Short sentences.** Punchy. One idea per line. Aggressive line breaks.
4. **No fluff.** Every word earns its place.
5. **End with a hook** — question, cliffhanger, or CTA that drives replies/retweets.
6. **Max 1-2 hashtags.** Best performers: `#GenAI` `#AIAgents` `#MCP` `#BuildInPublic` `#MachineLearning` `#LLM` `#Python`
7. **For threads:** Use `🧵` on tweet 1. Number subsequent tweets `2/` `3/` etc. Each part ≤ 280 chars.

---

### Single Tweet Templates

#### PRODUCTION PAIN POINT
```
Your AI app just went down because [provider] had an outage.

Here's how to make it bulletproof with [X] lines of code:

[Solution or hook]

🧵
```

#### COST SAVINGS
```
We saved $[X]K/month on LLM costs with one config change.

Here's exactly how (with code):

🧵
```

#### QUICK TIP
```
This [timeframe] AI trick just saved me [time/effort]:

[Specific before → after]

[Tool or prompt used]
```

#### HOT TAKE
```
[Popular thing] is overrated.

Here's why [alternative] actually works better:

→ [Reason 1]
→ [Reason 2]
→ [Reason 3]

Change my mind.
```

#### BEFORE / AFTER
```
Before: [Problem / time spent]
After: [Solution / time saved]

The tool: [name]

Here's the exact workflow:
```

#### PREDICTION
```
Prediction: By end of [year], [specific capability] will be as common as [familiar thing].

Here's why:

→ [Reason 1]
→ [Reason 2]
→ [Reason 3]
```

#### RESULTS / PROOF
```
[Timeframe] ago, I [started doing X].

The results:

→ [Metric 1]: [result]
→ [Metric 2]: [result]
→ [Metric 3]: [result]

Here's exactly what I did:
```

#### MISTAKE STORY
```
I was wrong about [topic].

I thought [old belief].

But after [experience], here's what I now know:

[New insight]
```

---

### Thread Structure (5–8 Tweets)

#### Tweet 1 — Hook (≤ 200 chars)
Stop the scroll. Use a pain point, shocking stat, or bold claim. End with `🧵` to signal thread.

**Proven hook patterns:**
```
Your AI app just went down because OpenAI had an outage.
Here's how to make it bulletproof with 2 lines of code: 🧵
```
```
Switching between GPT-4, Claude, and Gemini used to require rewriting your entire codebase.
Now it takes 1 line: 🧵
```
```
It's only been [X] since [EVENT], and the results are already wild.
The [N] most impressive things I've seen: 🧵
```
```
Stop [common bad practice].
Every time you [do X], you're [losing time/money/reliability].
There's a better way: 🧵
```
```
[Tool] just shipped [feature].
Here's what it means for your AI apps: 🧵
```

#### Tweet 2 — Problem / Context
- Why this pain point matters for developers/builders
- Relatable frustration: cost, reliability, vendor lock-in, complexity
- No solution yet — build tension

#### Tweets 3–5 — Solution with Code or Steps
- One concept per tweet
- Reference screenshots: `[screenshot: code-snippet-1]`
- Emphasize simplicity: "2-line integration", "zero code changes"
- Show before → after where possible

#### Tweet 6 — Results / Benefits
```
What you get:
→ [Benefit 1]
→ [Benefit 2]
→ [Benefit 3]
→ [Benefit 4]

All through a single unified API.
```

#### Tweet 7 — CTA
```
Full docs / cookbook: [link]

⭐ Star on GitHub: [link]

Follow @[handle] for more [topic] tips.
```

---

### Code Snippet Guidelines

When the tweet involves a tool or technical workflow, include code formatted for screenshots.

**Rules:**
- **5–12 lines** — fits in a clean screenshot
- **Self-contained** — makes sense without extra context
- **Show the import** — brand/tool recognition
- **No long lines** — proper indentation, readable at a glance
- **Add a `#` comment** at the end to land the point: `# Auto-switches to Claude ✨`

**Template:**
```python
from [library] import [Client]

client = [Client](
    api_key="[key]",
    config={...}
)

response = client.[method](
    model="[model]",
    messages=[{"role": "user", "content": "Hello!"}]
)
# [What just happened in plain English] ✨
```

---

## Step 5: Output Format

### For a Single Tweet
```
**TWEET:**
[Full tweet, ready to copy-paste]

---

**WHY THIS WILL WORK:**
[2 sentences — scroll-stopper mechanic + engagement driver]

---

**REPLY HOOKS (pin as first comment):**
- [Hook 1 — question to spark replies]
- [Hook 2 — controversial follow-up]
- [Hook 3 — invite people to share their version]

---

**POSTING TIP:**
[Best time, visual to pair, whether to add a poll]
```

---

### For a Thread (also save as `.md` file when requested)

Use this exact file structure when generating a full thread or saving to a `tweets/` folder:

```markdown
# [Topic Title] - Tweet Thread

## Thread

**Tweet 1 (Hook):**
[content]

**Tweet 2:**
[content]

**Tweet 3:**
[content — reference screenshot if code]

**Tweet 4:**
[content]

**Tweet 5:**
[content]

**Tweet 6 (Results):**
[content]

**Tweet 7 (CTA):**
[content]

---

## Code Snippets for Screenshots

### code-snippet-1
[code block]

### code-snippet-2
[code block]

---

## Hashtags

[1–2 relevant hashtags]

---

## Posting Notes

- **Best times:** 9–10 AM or 6 PM in your audience's timezone
- **Engagement window:** Reply to every comment in the first 30 minutes
- **Visual:** Pair Tweet 1 with a screenshot or short demo video
- **Follow-up:** Reply to Tweet 1 with the cookbook/docs link after posting
```

**File naming convention:** `{topic-slug}-tweet.md`

Examples: `gateway-fallbacks-tweet.md` · `claude-code-review-tweet.md` · `rag-vs-prompting-tweet.md`

---

## What NOT to Do

- ❌ Generic inspirational quotes with no specifics
- ❌ Vague claims ("AI is changing everything")
- ❌ Self-promotion without value ("Check out my tool")
- ❌ More than 2 hashtags
- ❌ Starting with "I think" or "In my opinion"
- ❌ Rehashing old news without a new angle or take
- ❌ Long paragraphs — line breaks are free, use them
- ❌ Code snippets longer than 12 lines in screenshots
- ❌ Threads longer than 8 tweets — split into a series instead

---

## Examples

### Example 1 — Production Pain Point Thread
**Input:** "Write a tweet thread about AI app reliability and fallbacks"

**Output:**

```markdown
# AI Gateway Fallbacks - Tweet Thread

## Thread

**Tweet 1 (Hook):**
Your AI app crashed because OpenAI had a 30-minute outage.

Meanwhile, apps using an AI Gateway stayed up with zero downtime.

Here's how to add automatic fallbacks in 2 minutes: 🧵

**Tweet 2:**
The problem: most apps hardcode a single LLM provider.

When that provider goes down, your entire app goes down.

The fix? An AI Gateway that auto-routes to backup providers.

**Tweet 3:**
Step 1: swap your OpenAI client for a gateway client.

[screenshot: code-snippet-1]

Your existing code works unchanged. Same API surface.

**Tweet 4:**
Step 2: add a fallback config.

[screenshot: code-snippet-2]

Now if GPT-4 fails → auto-switches to Claude.
Zero code changes. Zero downtime.

**Tweet 5:**
What you get for free:
→ Automatic retries (up to 5x)
→ Load balancing across providers
→ Real-time cost tracking
→ 50+ safety guardrails

All through one unified API.

**Tweet 6 (CTA):**
Full cookbook with working code: [docs link]
⭐ Star on GitHub: [github link]

Follow for more production AI tips.

---

## Code Snippets for Screenshots

### code-snippet-1
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
# Drop-in OpenAI replacement, with superpowers ✨
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
# If OpenAI fails → auto-switches to Claude ✨
```

---

## Hashtags

#AIGateway #LLM

---

## Posting Notes

- **Best times:** 10 AM or 6 PM IST / 9 AM or 1 PM EST
- **Engagement window:** Reply to every comment in the first 30 minutes
- **Visual:** Pair Tweet 1 with a short demo screen recording
- **Follow-up:** Reply to Tweet 1 with the cookbook link after posting
```

---

### Example 2 — Hot Take (Single Tweet)
**Input:** "Tweet about how RAG is overused"

```
TWEET:
RAG is overrated.

I've built 30+ AI apps. Most didn't need it.

Here's what works for 80% of use cases instead:

→ Well-structured system prompts
→ Context injection at runtime
→ Smaller, focused models

RAG adds complexity. Start without it.

Change my mind 👇

#GenAI

---

WHY THIS WILL WORK:
Opens with a bold falsifiable claim that practitioners will either strongly agree or disagree with — both reactions drive replies. The numbered alternatives give people something concrete to argue against.

---

REPLY HOOKS:
- "What's the most complex use case where you actually needed RAG?"
- "Anyone switched away from RAG and not looked back?"
- "At what data size does RAG actually become worth it?"

---

POSTING TIP:
Post Tuesday–Thursday, 9–11 AM. No image needed — the take is the content. Consider a follow-up poll: "Do you use RAG in production? Yes / No / Sometimes"
```

---

### Example 3 — Quick Tip with Code (Single Tweet)
**Input:** "Tweet a tip about using AI for code reviews"

```
TWEET:
This prompt saves my team 4 hours of code review per week:

"You are a senior engineer. Review this code for:
- Security vulnerabilities
- Performance bottlenecks
- Edge cases
- Readability

Be specific. Give exact line numbers."

Paste your PR diff. Done.

#BuildInPublic

---

CODE SNIPPET (for screenshot):
```python
prompt = """You are a senior engineer.
Review this code for:
- Security vulnerabilities
- Performance bottlenecks
- Edge cases + error handling
- Readability

Be specific. Reference line numbers."""

response = client.chat.completions.create(
    model="gpt-4o",
    messages=[
        {"role": "system", "content": prompt},
        {"role": "user", "content": pr_diff}
    ]
)
# Instant senior engineer review ✨
```

WHY THIS WILL WORK:
The specific time savings number (4 hours) is credible and relatable. The prompt is complete enough to copy immediately — zero friction to try it.

REPLY HOOKS:
- "What model do you get the best code reviews from?"
- "Anyone using this in a CI/CD pipeline automatically?"
- "Drop your version of this prompt below 👇"

POSTING TIP:
Screenshot the code snippet and attach as image to the tweet. Post Monday morning when developers are starting their week.
```