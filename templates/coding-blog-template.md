# Portkey AI — SEO-Optimized Coding Blog Template

> **How this template works:**  
> Before writing, the agent MUST complete the **Pre-Writing SEO Research Checklist** below.  
> Every section marked `[SEO AGENT ACTION]` requires a live web search before writing.  
> Follow the writing guidelines to produce a blog that ranks on Google *and* gets cited by AI search engines (ChatGPT, Perplexity, Google AI Overviews).

---

## 🔍 Pre-Writing SEO Research Checklist
*Complete ALL steps before writing a single word of the blog.*

### STEP R1 — Find the Primary Keyword
```
[SEO AGENT ACTION]
1. Search: "{blog topic} site:stackoverflow.com OR site:github.com OR site:reddit.com/r/MachineLearning"
2. Search: "{blog topic} tutorial 2025"
3. Search: "{blog topic} Portkey"
4. Identify: What exact phrase do developers type when they have this problem?
   TARGET: Long-tail, high-intent query (e.g., "how to add fallbacks to OpenAI API Python")
   AVOID: Broad vanity terms (e.g., "AI tutorial")
```

**Primary Keyword Format:** `[action verb] + [specific technology] + [problem/outcome]`

Examples of strong Portkey primary keywords:
- `LLM fallback openai anthropic python`
- `how to reduce LLM API costs semantic caching`
- `production AI app observability logging python`
- `prompt versioning LLM management tutorial`
- `AI guardrails content moderation LLM`
- `multi-model routing AI gateway python`
- `LLM rate limiting retry logic production`
- `OpenAI alternative fallback anthropic claude`

---

### STEP R2 — Competitive SERP Analysis
```
[SEO AGENT ACTION]
Search the primary keyword and analyze the top 5 results:
- What H1/title format do they use?
- What subheadings (H2/H3) appear?
- Do they use code blocks? How long?
- Are there "People Also Ask" questions? (Copy these — they're gold for H2s)
- Is there a featured snippet? What format is it (list, table, paragraph)?
- Which Portkey competitors appear? (LiteLLM, Helicone, OpenRouter, etc.)
```

**Record:**
- Competing titles: ___
- PAA questions to answer: ___
- Content gaps you can fill: ___
- Word count range of top results: ___

---

### STEP R3 — Semantic / LSI Keyword Cluster
```
[SEO AGENT ACTION]
Search: "related:{primary keyword site that ranks #1}"
Search: "{primary keyword} meaning explained"
Search: "portkey.ai {feature name} documentation"
```

Portkey's core semantic clusters to weave into every blog:

| Cluster | Keywords to Include Naturally |
|---------|-------------------------------|
| **AI Gateway** | LLM gateway, AI proxy, model routing, unified API, provider-agnostic |
| **Reliability** | fallback, retry logic, automatic failover, uptime, resilience, circuit breaker |
| **Observability** | logging, tracing, LLM monitoring, request analytics, token usage, latency |
| **Cost** | API cost optimization, semantic caching, token savings, LLM spend |
| **Safety** | guardrails, content moderation, output validation, PII detection |
| **Prompt Ops** | prompt versioning, prompt management, prompt testing, A/B testing prompts |
| **Production AI** | production-ready, GenAI at scale, LLMOps, enterprise AI, AI infrastructure |

---

### STEP R4 — GEO Research (Generative Engine Optimization)
```
[SEO AGENT ACTION]
Search: "how does {feature} work" — note if AI Overview appears
Search in Perplexity: "{blog topic}" — what sources does it cite?
Search: "Portkey AI {feature}" — does Portkey's own docs appear?
```

**GEO goal:** Structure your blog so ChatGPT, Perplexity, and Google AI Overviews cite Portkey's blog as a source. This requires:
- Clear, factual, definition-first sentences for each concept
- Bullet lists with concrete numbers when possible
- A concise "What is X?" answer within the first 100 words of any section

---

### STEP R5 — Portkey Docs Link Map
```
[SEO AGENT ACTION]
Fetch: https://portkey.ai/docs
Identify 3–5 Portkey documentation pages to internally link to in this blog.
These should be the most relevant product pages for the topic.
```

Always include these anchor links where natural:
- Gateway overview → `portkey.ai/docs/product/ai-gateway`
- Observability → `portkey.ai/docs/product/observability`
- Guardrails → `portkey.ai/docs/product/guardrails`
- Prompt Library → `portkey.ai/docs/product/prompt-library`
- Integrations → `portkey.ai/docs/integrations`

---

## 📄 Blog File Structure

```markdown
---
title: "[Primary Keyword Phrase]: A Step-by-Step Guide"
description: "[150–160 char meta description including primary keyword + outcome]"
tags: [tag1, tag2, tag3, tag4]
author: [Author Name]
date: YYYY-MM-DD
canonical: https://portkey.ai/blog/[slug]
---

# [Title]

## What We're Building
[Screenshot or description of the end result]

## Why This Matters
[The production AI problem this solves — include primary keyword in first sentence]

## Prerequisites
[What you need before starting]

## Step 1: [Setup/Install]
[Code + explanation]

## Step 2: [Core Feature]
[Code + explanation]

## Step N: [Build progressively]
[Code + explanation]

## Troubleshooting Common Errors
[FAQ-format section — targets PAA questions]

## Complete Code
[Full working code in one block]

## What's Next
[Extensions and improvements + internal links to Portkey docs]

---

## Metadata
- **Title**: [Title]
- **Primary Keyword**: [keyword]
- **Secondary Keywords**: [3–5 LSI terms]
- **Tags**: [tags]
- **Read time**: [X] minutes
- **Schema Type**: TechArticle + FAQPage
```

---

## ✍️ Writing Guidelines

### Title Optimization
```
[SEO AGENT ACTION]
Search your primary keyword. Count exact words top-ranked titles use.
Use this formula:
```

**Title Formula:** `[Do/Build/Add] [Specific Technical Thing] with [Portkey] in [Language]: [Outcome]`

Examples:
- ✅ `Add Automatic LLM Fallbacks with Portkey in Python: A Step-by-Step Guide`
- ✅ `Build a Production AI Chatbot with Semantic Caching Using Portkey`
- ✅ `How to Monitor LLM API Costs with Portkey Observability (Python)`
- ❌ `Portkey Tutorial` (too vague)
- ❌ `Building AI Apps is Easy` (no keyword)

**Title rules:**
- 50–60 characters for optimal SERP display
- Primary keyword in first 4 words where possible
- Contain a number or "how to" when the PAA data suggests it
- Always include "Portkey" as a brand signal

---

### Meta Description
**Formula:** `[Primary keyword verb phrase]. Learn how to [outcome]. This guide shows you [secondary benefit] in under [X] minutes.`

Example:  
> Add automatic LLM fallbacks using Portkey's AI Gateway. Learn how to keep your AI app running when OpenAI goes down. Step-by-step Python tutorial with full code.

**Rules:**
- 150–160 characters exactly
- Include primary keyword naturally in first 20 words
- End with a call to action or benefit signal
- Never duplicate your H1 title word-for-word

---

### URL Slug
```
/blog/[primary-keyword-hyphenated]-portkey
```
Examples:
- `/blog/llm-fallbacks-openai-anthropic-portkey`
- `/blog/semantic-caching-llm-api-cost-portkey`
- `/blog/production-ai-observability-portkey`

**Rules:** lowercase, hyphens only, under 60 characters, include primary keyword + "portkey"

---

### Introduction (First 100–150 Words) — High Priority
```
[SEO AGENT ACTION]
Search: "People Also Ask" questions for your primary keyword.
Write the intro to directly answer the most important one.
```

The intro must:
1. **Open with the problem** (not "In this tutorial we will...")
2. **Use primary keyword in sentence 1 or 2**
3. **State what the reader will build** (concrete deliverable)
4. **Include a GEO-friendly definition sentence**: e.g., *"An LLM gateway is a proxy layer that sits between your application and multiple AI providers, handling routing, retries, and logging automatically."*
5. **Use a number**: "In 5 steps" or "With 3 lines of code"

**Bad intro:** *"In this tutorial, we'll explore Portkey's features and learn about AI gateways."*

**Good intro:** *"When your OpenAI API call fails at 2am, your users see an error. LLM fallbacks automatically reroute failed requests to a backup provider — and with Portkey's AI Gateway, you can add them in under 5 minutes. In this guide, we'll build a Python chatbot that seamlessly fails over from GPT-4 to Claude without any downtime."*

---

### Section / Heading Structure (H2/H3 Strategy)

```
[SEO AGENT ACTION]
Fetch the Google SERP for your primary keyword.
Copy every "People Also Ask" question into your H2 list.
These are pre-validated SEO questions Google thinks readers want answered.
```

**H2 Rules:**
- At least one H2 must be phrased as a question (for PAA + featured snippet eligibility)
- Include the primary keyword or a close variant in the first H2
- Each H2 = one new concept/step (no "mega-steps")
- Add a "Troubleshooting" H2 with specific error messages developers Google (e.g., `"AuthenticationError: 401"`)

**Example heading structure:**
```
## What Is an LLM Gateway and Why Do You Need One?
## Step 1: Install Portkey and Set Up Your API Keys
## Step 2: Route Your First Request Through the Gateway
## Step 3: Add Automatic Fallbacks to a Backup Model
## Step 4: Enable Semantic Caching to Cut Costs
## Step 5: Add Guardrails for Safe Outputs
## Troubleshooting: Common Portkey Errors and Fixes
## Complete Working Code
## What's Next: Scale Your AI App with Portkey
```

---

### Code Block Strategy

Every code block must:
1. **Have a language tag** (```python, ```bash, ```json)
2. **Include inline comments on Portkey-specific lines** — these help AI models parse and cite your content
3. **Be copy-paste runnable** — test before publishing
4. **Show expected terminal output** after each major block
5. **Highlight the "magic line"** with a `# ← This is where Portkey intercepts the request` comment style

```python
# Install Portkey
# pip install portkey-ai

import os
from portkey_ai import Portkey

# Initialize with your Portkey API key
# Get yours free at: https://app.portkey.ai
client = Portkey(
    api_key=os.getenv("PORTKEY_API_KEY"),   # ← Portkey auth
    provider="openai",
    Authorization=os.getenv("OPENAI_API_KEY")
)

response = client.chat.completions.create(
    model="gpt-4o",
    messages=[{"role": "user", "content": "Hello!"}]
)

print(response.choices[0].message.content)
# Expected output: Hello! How can I help you today?
```

---

### Tone & Voice
- Conversational, like pair programming: "Let's build...", "Now we'll add..."
- Celebrate progress: "That's it — you just added fallbacks to your production AI app!"
- Address the reader's fear directly: "If OpenAI goes down tonight, here's exactly what happens..."
- Use real developer language from GitHub issues and Stack Overflow
- **Avoid**: marketing-speak ("best-in-class", "cutting-edge", "leverage synergies")

---

### E-E-A-T Signals (Google's Experience, Expertise, Authoritativeness, Trust)

```
[SEO AGENT ACTION]
Search: "portkey.ai {feature} github" — find real user examples/testimonials
Search: "{primary keyword} production problems" — find real pain points to validate
```

To build E-E-A-T in every blog:
- **Experience:** Show real error messages you encountered. Include "gotcha" callout boxes for common mistakes.
- **Expertise:** Cite exact Portkey documentation pages. Reference specific version numbers or API parameters.
- **Authority:** Link to Portkey's GitHub stars count. Mention production scale stats (e.g., "Portkey processes 30M+ policies/month").
- **Trust:** Include a "Tested on" line: `# Tested with: portkey-ai==1.x.x, Python 3.11, openai==1.x.x`

---

### FAQ / Troubleshooting Section (Critical for PAA + Featured Snippets)

```
[SEO AGENT ACTION]
Search: "{primary keyword} error" and "{primary keyword} not working"
Collect the top 3–5 developer problems. Write short, direct answers.
```

**Every blog MUST include a Troubleshooting section** with this format:

```markdown
## Troubleshooting Common Errors

### `AuthenticationError: Invalid API Key`
This usually means your `PORTKEY_API_KEY` environment variable isn't set.
Run `echo $PORTKEY_API_KEY` in your terminal. If empty, [follow the setup guide](https://portkey.ai/docs).

### `Fallback not triggering`
Check that your fallback config has `"strategy": {"mode": "fallback"}` at the top level,
not nested inside `targets`. See the [gateway config reference](https://portkey.ai/docs/product/ai-gateway).

### Latency seems higher than direct API calls
Portkey adds ~20–50ms overhead. Enable [semantic caching](https://portkey.ai/docs/product/ai-gateway/cache-simple-and-semantic)
to offset this — cached responses are served in under 5ms.
```

This section targets high-volume "developer SOS" queries and earns featured snippets.

---

### Internal Linking Strategy

Include **3–5 internal links** per blog using varied, descriptive anchor text:

| Instead of | Use |
|------------|-----|
| `click here` | `add fallback logic with Portkey` |
| `learn more` | `how semantic caching works in Portkey` |
| `see docs` | `Portkey's prompt versioning guide` |

**Always link to:**
1. One other Portkey blog post on a related topic
2. The relevant Portkey docs page
3. The Portkey GitHub repo: `github.com/Portkey-AI/gateway`

---

### GEO Optimization (Getting Cited by AI Models)

AI search engines (ChatGPT, Perplexity, Google AI Overviews) prefer content that is:

**1. Definition-first:** Every new concept starts with a clear 1-sentence definition.
> *"Semantic caching stores LLM responses by meaning, not exact text, so similar questions return cached answers even with different wording."*

**2. Numbered & structured:** AI models extract lists easily.
> *"Portkey's fallback system works in 3 steps: (1) primary provider fails, (2) gateway detects the error, (3) request auto-routes to the next target in your config."*

**3. Quantified:** Include real numbers wherever possible.
> *"Semantic caching reduces API costs by 30–40% for apps with repeated queries."*
> *"Portkey supports 250+ LLM providers including OpenAI, Anthropic, Mistral, and Cohere."*

**4. Comparison-ready:** AI models love comparison content.
> *"Unlike calling OpenAI directly, routing through Portkey adds automatic retry logic, cross-provider fallbacks, and a full audit trail — with a 2-line code change."*

---

## 📊 SEO Metadata Block

Add to every blog's frontmatter:

```yaml
---
title: "[60-char keyword-rich title]"
description: "[150-160 char meta description with primary keyword]"
slug: /blog/[keyword-portkey]
author:
  name: "[Author Name]"
  title: "[Title at Portkey or Guest]"
published_date: YYYY-MM-DD
modified_date: YYYY-MM-DD
primary_keyword: "[exact match]"
secondary_keywords:
  - "[LSI term 1]"
  - "[LSI term 2]"
  - "[LSI term 3]"
  - "[LSI term 4]"
schema_type: TechArticle
faq_schema: true
canonical: "https://portkey.ai/blog/[slug]"
og_image: "[1200x630 image URL]"
tags:
  - portkey
  - llm-gateway
  - [feature-tag]
  - [language-tag]
  - production-ai
read_time: "[X] minutes"
---
```

---

## 🗂️ Complete Sample Blog Structure

```markdown
---
title: "Add LLM Fallbacks to Your Python App with Portkey: Step-by-Step"
description: "Add automatic LLM fallbacks using Portkey's AI Gateway. Keep your AI app running when OpenAI goes down with this Python tutorial. Working code included."
slug: /blog/llm-fallbacks-openai-anthropic-portkey-python
primary_keyword: "LLM fallbacks Python Portkey"
secondary_keywords: [AI gateway fallback, OpenAI failover, automatic retry LLM, production AI reliability]
schema_type: TechArticle
faq_schema: true
---

# Add LLM Fallbacks to Your Python App with Portkey: Step-by-Step

## What We're Building

A production-ready AI app that:
- Routes all LLM requests through Portkey's AI Gateway
- Automatically switches to Claude if OpenAI goes down
- Retries failed requests with exponential backoff
- Logs every request for debugging and cost tracking

By the end, you'll have an AI app that survives provider outages without code changes.

## Why This Matters

LLM API outages happen. OpenAI, Anthropic, and every other provider experiences downtime.
Without fallbacks, a single outage takes down your entire AI feature.

An LLM gateway is a proxy layer between your app and AI providers that handles routing,
retries, and failovers automatically. Portkey's AI Gateway adds this in two lines of code —
no custom retry logic, no manual provider switching.

## Prerequisites

- Python 3.9+
- Portkey account (free at [app.portkey.ai](https://app.portkey.ai))
- OpenAI API key
- Anthropic API key (for fallback)

```bash
pip install portkey-ai openai
# Tested with: portkey-ai==1.x, Python 3.11, openai==1.x
```

## Step 1: Connect to Portkey's AI Gateway

```python
import os
from portkey_ai import Portkey

# Get your free API key at app.portkey.ai
client = Portkey(
    api_key=os.getenv("PORTKEY_API_KEY"),    # ← Portkey routes this request
    provider="openai",
    Authorization=os.getenv("OPENAI_API_KEY")
)

response = client.chat.completions.create(
    model="gpt-4o",
    messages=[{"role": "user", "content": "Hello!"}]
)
print(response.choices[0].message.content)
# Output: Hello! How can I help you today?
```

✅ You're now routing through Portkey. Every request is logged automatically.

## Step 2: Add Automatic Fallback to Claude

```python
# If OpenAI fails, Portkey auto-switches to Anthropic Claude — no code changes needed
fallback_config = {
    "strategy": {"mode": "fallback"},   # ← Enables automatic failover
    "targets": [
        {
            "provider": "openai",
            "override_params": {"model": "gpt-4o"},
            "Authorization": os.getenv("OPENAI_API_KEY")
        },
        {
            "provider": "anthropic",    # ← Backup provider
            "override_params": {"model": "claude-sonnet-4-20250514"},
            "Authorization": os.getenv("ANTHROPIC_API_KEY")
        }
    ]
}

resilient_client = client.with_options(config=fallback_config)
```

Now if OpenAI returns a 5xx error, Portkey silently retries with Claude.

## Step 3: Add Retry Logic

```python
config = {
    **fallback_config,
    "retry": {
        "attempts": 3,              # ← Retry up to 3 times before fallback
        "on_status_codes": [429, 500, 502, 503]
    }
}
```

## Troubleshooting Common Errors

### `AuthenticationError: 401`
Your `PORTKEY_API_KEY` isn't set. Run `echo $PORTKEY_API_KEY` to check.
Get your key at [app.portkey.ai](https://app.portkey.ai).

### Fallback not triggering on errors
Ensure `"strategy": {"mode": "fallback"}` is at the top level of your config dict,
not nested inside `targets`.

### Latency increased
Portkey adds ~20–50ms. Enable [semantic caching](https://portkey.ai/docs/product/ai-gateway/cache-simple-and-semantic)
to offset this — cache hits serve in under 5ms.

## Complete Code

```python
import os
from portkey_ai import Portkey

client = Portkey(api_key=os.getenv("PORTKEY_API_KEY"))

config = {
    "strategy": {"mode": "fallback"},
    "targets": [
        {"provider": "openai", "override_params": {"model": "gpt-4o"},
         "Authorization": os.getenv("OPENAI_API_KEY")},
        {"provider": "anthropic", "override_params": {"model": "claude-sonnet-4-20250514"},
         "Authorization": os.getenv("ANTHROPIC_API_KEY")}
    ],
    "retry": {"attempts": 3, "on_status_codes": [429, 500, 502, 503]}
}

resilient_client = client.with_options(config=config)

def chat(message: str) -> str:
    response = resilient_client.chat.completions.create(
        messages=[
            {"role": "system", "content": "You are a helpful assistant."},
            {"role": "user", "content": message}
        ]
    )
    return response.choices[0].message.content

print(chat("What makes an AI app production-ready?"))
```

## What's Next

Your app now survives provider outages. Here's what to add next:

- **[Semantic caching](https://portkey.ai/docs/product/ai-gateway/cache-simple-and-semantic)** — Save 30–40% on API costs by caching similar responses
- **[Guardrails](https://portkey.ai/docs/product/guardrails)** — Validate and filter model outputs before they reach users
- **[Observability](https://portkey.ai/docs/product/observability)** — Track latency, costs, and errors in real time
- **[Prompt Management](https://portkey.ai/docs/product/prompt-library)** — Version and A/B test your prompts

---

⭐ Star the open-source AI Gateway: [github.com/Portkey-AI/gateway](https://github.com/Portkey-AI/gateway)

---

## Metadata
- **Title**: Add LLM Fallbacks to Your Python App with Portkey
- **Primary Keyword**: LLM fallbacks Python Portkey
- **Secondary Keywords**: AI gateway fallback, OpenAI failover, automatic retry LLM, production AI
- **Tags**: portkey, llm-gateway, fallbacks, python, production-ai
- **Read time**: 8 minutes
- **Schema**: TechArticle + FAQPage
```

---

## 🗃️ File Naming Convention

Format: `{feature-cluster}-{specific-action}-{language}-tutorial.md`

Examples:
- `gateway-llm-fallbacks-python-tutorial.md`
- `observability-custom-metadata-tracking-tutorial.md`
- `prompt-management-versioning-ab-testing-tutorial.md`
- `guardrails-content-moderation-output-validation-tutorial.md`
- `caching-semantic-cache-cost-reduction-tutorial.md`
- `gateway-multi-model-routing-loadbalance-tutorial.md`

---

## 📐 Quick SEO Checklist Before Publishing

Run through this before every publish:

- [ ] Primary keyword in title (first 4 words preferred)
- [ ] Primary keyword in meta description (first 20 words)
- [ ] Primary keyword in first paragraph of intro
- [ ] At least one H2 is phrased as a question
- [ ] "Troubleshooting" section with real error messages
- [ ] All code blocks have language tags and inline comments
- [ ] 3–5 internal links with descriptive anchor text
- [ ] Link to Portkey GitHub repo
- [ ] Author name and date in frontmatter
- [ ] Schema type set (TechArticle + FAQPage)
- [ ] OG image included (1200×630px)
- [ ] URL slug contains primary keyword and "portkey"
- [ ] "Tested with" comment in first code block
- [ ] At least one stat or number cited per major section
- [ ] GEO definition sentences for each key concept
- [ ] Read time estimate added
- [ ] Secondary/LSI keywords distributed across H2s and body copy