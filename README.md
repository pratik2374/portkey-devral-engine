# 🚀 Portkey AI — Content Engine

> An AI-powered content generation engine for **Portkey AI** DevRel — producing cookbooks, tweets, LinkedIn posts, technical blogs, code snippets, coding tutorials, and programming guides at scale.

## 🎯 What This Is

This is a **Claude-powered content engine** (agent skill) specifically built for Portkey AI's developer relations. Feed it a weekly content plan, and it generates production-ready content across **7 formats** — all in Portkey's voice, with accurate SDK code, and optimized for each platform.

### The DevRel Value Proposition

| Problem | Solution |
|---------|----------|
| Content creation is slow and inconsistent | Automated engine generates all formats from a single plan |
| Code examples get outdated | Templates enforce latest `portkey_ai` SDK patterns |
| Multi-platform posting is tedious | One topic → cookbook + tweet + LinkedIn + blog simultaneously |
| Brand voice varies across authors | Centralized voice guidelines ensure consistency |
| New features need documentation fast | Topic-driven workflow enables same-day content for launches |

## 📁 Project Structure

```
portkey-content-engine/
├── CLAUDE.md                          # Agent instructions (the brain)
├── README.md                          # This file
├── config/
│   └── settings.md                    # Brand info, defaults, env vars
├── templates/
│   ├── cookbook-template.md            # Jupyter notebook cookbooks
│   ├── tweet-thread-template.md       # X/Twitter threads
│   ├── linkedin-post-template.md      # LinkedIn posts
│   ├── technical-blog-template.md     # Deep-dive technical blogs
│   ├── code-snippet-template.md       # Multi-language code snippets
│   ├── coding-blog-template.md        # Tutorial-style coding blogs
│   └── programming-guide-template.md  # Language integration guides
├── plans/
│   └── week-1.md                      # Weekly content plans
├── topics/
│   └── week-1-topics.md               # Trending topics & news
└── output/
    └── samples/                       # Sample generated content
```

## 🛠 Content Types

| # | Type | Format | Platform |
|---|------|--------|----------|
| 1 | **Cookbooks** | `.ipynb` | GitHub, Docs |
| 2 | **Tweet Threads** | `.md` | X/Twitter |
| 3 | **LinkedIn Posts** | `.md` | LinkedIn |
| 4 | **Technical Blogs** | `.md` | Blog, Dev.to, Medium |
| 5 | **Code Snippets** | `.md` | Docs, GitHub, Social |
| 6 | **Coding Blogs** | `.md` | Blog, Dev.to |
| 7 | **Programming Guides** | `.md` | Docs |

## 📊 Content Buckets

| Bucket | Focus Area |
|--------|-----------|
| AI Gateway & Routing | Fallbacks, retries, load balancing, configs |
| Observability & Analytics | Logs, traces, dashboards, cost tracking |
| Guardrails & Security | Input/output validation, PII redaction |
| Agent Integrations | OpenAI Agents, CrewAI, LangChain, Agno |
| Advanced Patterns | Caching, MCP Gateway, conditional routing |
| Getting Started | SDK setup, first API call, quickstart |

## 🚀 How to Use

### 1. Set up environment
```bash
export PORTKEY_API_KEY=your_portkey_key
export OPENAI_API_KEY=your_openai_key
```

### 2. Create a weekly plan
Edit `plans/week-X.md` with your content schedule.

### 3. Run the engine
Open this project in an AI coding assistant (Claude Code, Cursor, etc.) and say:
```
Read plans/week-1.md and topics/week-1-topics.md, then generate all content files to output/week-1/
```

### 4. Review & publish
All generated content lands in `output/week-X/` organized by format.

## 🔑 Key Features

- **7 content formats** from a single topic
- **Portkey SDK-accurate** code in every example
- **Multi-language** snippets (Python, JavaScript, cURL)
- **Platform-optimized** (character limits, hashtags, carousels)
- **Brand-consistent** voice across all content
- **Production-focused** messaging (reliability, observability, scale)

## 📚 Resources

- [Portkey AI Docs](https://portkey.ai/docs/)
- [AI Gateway (GitHub)](https://github.com/Portkey-AI/gateway)
- [Portkey Blog](https://portkey.ai/blog)
- [@PortkeyAI on X](https://x.com/PortkeyAI)
- [Portkey on LinkedIn](https://www.linkedin.com/company/portkey-ai/)

---

*Built with ❤️ to scale Portkey AI's developer community*
