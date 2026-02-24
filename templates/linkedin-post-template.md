# LinkedIn Post Template

Use this structure when generating LinkedIn posts (`.md` files in `linkedin/` folder) for Portkey AI.

---

## File Structure

```markdown
# [Title] - LinkedIn Post

## Post

[Main post content - 1300-2000 characters]

---

## First Comment

Link: [Portkey docs/blog link]
[Brief description]

---

## Carousel Slides (if applicable)

Slide 1: [Title]
Slide 2-N: [Content]

---

## Posting Notes

[Timing, hashtags, engagement strategy]
```

---

## Post Structure (1300-2000 chars)

### Opening Hook (1-2 lines)
- Production AI insight or war story
- Surprising stat about LLM costs/reliability
- Industry trend observation
- Question that resonates with AI builders

### Context/Problem (2-3 lines)
- What teams struggle with when deploying LLMs
- Why this matters for production AI
- Relatable scenario (outages, cost spikes, vendor lock-in)

### Main Content (5-10 lines)
- Portkey's approach / solution
- Technical insights with business impact
- Use line breaks for readability
- Can include 3-5 line code snippets

### Key Takeaways (3-5 bullets)
- Actionable insights for AI teams
- Start each with action verb
- Keep each to one line

### Engagement CTA (1-2 lines)
- Question for the AI engineering audience
- Invite discussion about production challenges
- No external links in main post

---

## Hook Formulas

### Pattern 1: Production War Story
```
We processed 10B+ tokens through our AI Gateway last month.

Here are the 3 patterns that separate resilient AI apps from fragile ones:
```

### Pattern 2: Industry Observation
```
Every enterprise AI team I talk to has the same problem:

They're locked into a single LLM provider and terrified of switching.
```

### Pattern 3: Data-Driven Insight
```
We tracked $93M in LLM spending across our platform last year.

The #1 cost driver wasn't the models — it was redundant API calls.
```

### Pattern 4: Behind the Scenes
```
Our gateway handles 2 billion+ requests.

Here's the architecture that makes sub-millisecond routing possible:
```

### Pattern 5: Contrarian Take
```
"Just use the OpenAI API directly."

That advice costs companies thousands in unnecessary downtime every month. Here's why:
```

### Pattern 6: Prompt Management
```
Stop hardcoding prompts in your codebase.

Every time you change a word, you're waiting on a deployment. Here is the modern way:
```

### Pattern 7: Observability
```
Are you flying blind with your LLM usage in production?

If you can't tell which user generated which cost, you have a problem. Here's how to fix it:
```

---

## Formatting Guidelines

1. **Line breaks matter**: Use them liberally for readability
2. **No walls of text**: Max 3-4 lines before a break
3. **Emojis sparingly**: 2-3 max, use for visual breaks
4. **No links in post**: Put in first comment
5. **Bullet points**: Use for lists, keep short
6. **Code snippets**: Only if very short (3-5 lines max)

---

## Sample Complete Post

```markdown
# AI Gateway for Production - LinkedIn Post

## Post

We processed 10B+ tokens through our AI Gateway last month.

Here are the 3 reliability patterns every AI team should implement:

Most teams build their AI apps with a direct connection to one LLM provider.

When that provider has an outage — and they all do — the entire app goes down.

Here's what production-ready AI infrastructure looks like:

1️⃣ Automatic Fallbacks
→ If GPT-4 fails, auto-route to Claude
→ Zero code changes, just a config update
→ Your users never notice

2️⃣ Smart Caching
→ Cache identical requests (simple or semantic)
→ Typical savings: 30-40% on API costs
→ Bonus: faster response times

3️⃣ Guardrails at the Gateway
→ Validate LLM outputs before they reach users
→ 50+ pre-built checks for PII, toxicity, accuracy
→ Block bad responses, retry automatically

The key insight?

These patterns belong at the infrastructure layer, not in your application code.

An AI Gateway handles all of this with a single config — no code rewrites needed.

Key takeaways:
• Start with fallbacks — they're the highest ROI reliability investment
• Add caching early — the savings compound fast
• Put guardrails at the gateway, not in your app logic

What's the #1 reliability challenge you face with LLMs in production?

---

## First Comment

Full guide with code examples:
https://portkey.ai/docs/product/ai-gateway

Open-source gateway (17K+ stars):
https://github.com/Portkey-AI/gateway

---

## Carousel Slides (optional)

Slide 1: "3 Reliability Patterns for Production AI"
Slide 2: "Pattern 1: Automatic Fallbacks" (diagram: Provider A fails → route to Provider B)
Slide 3: "Pattern 2: Smart Caching" (before/after cost comparison)
Slide 4: "Pattern 3: Gateway Guardrails" (flow diagram)
Slide 5: "The Architecture" (AI Gateway between app and providers)
Slide 6: "Try it → link in comments"

---

## Posting Notes

- Best times: 8 AM or 12 PM IST (Tuesday-Thursday)
- Hashtags in comment: #AI #LLM #ProductionAI #AIInfrastructure
- Reply to comments within first 2 hours
- Tag CTOs, AI engineers, and DevOps leads when relevant
```

---

## Content Type Guidelines

### For Technical Architecture
- Lead with scale numbers (requests processed, tokens routed)
- Include architecture diagrams in carousel
- End with "what's your experience?"

### For Feature Announcements
- Lead with the problem it solves
- Provide your team's perspective
- End with "how would you use this?"

### For Comparisons / Analysis
- Lead with the context / why it matters
- Structure as clear before/after
- End with your recommendation

### For Customer Stories
- Lead with the business impact
- Share specific metrics (latency, cost, uptime)
- End with a question for the audience

---

## File Naming

Format: `{bucket}-{short-title}-linkedin.md`

Examples:
- `gateway-reliability-patterns-linkedin.md`
- `observability-cost-tracking-linkedin.md`
- `agents-production-monitoring-linkedin.md`
- `advanced-mcp-gateway-linkedin.md`
