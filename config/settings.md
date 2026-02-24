# Content Engine Settings

## Brand Information

```yaml
brand_name: "Portkey AI"
tagline: "The AI Gateway for Production LLM Apps"
description: "Portkey is a comprehensive AI Gateway that helps developers route to 250+ LLMs with reliability, observability, and guardrails."

# Links
website: "https://portkey.ai"
docs: "https://portkey.ai/docs/"
github_gateway: "https://github.com/Portkey-AI/gateway"
github_sdk_python: "https://github.com/Portkey-AI/portkey-python-sdk"
github_sdk_js: "https://github.com/Portkey-AI/portkey-node-sdk"
blog: "https://portkey.ai/blog"
twitter_handle: "@PortkeyAI"
twitter_url: "https://x.com/PortkeyAI"
linkedin_url: "https://www.linkedin.com/company/portkey-ai/"
discord: "https://discord.gg/DD7vgKK299"
community: "https://portkey.wiki/community"

# CTAs to include in content
cta_github: "⭐ Star our gateway: github.com/Portkey-AI/gateway"
cta_twitter: "Follow @PortkeyAI for production AI tips"
cta_docs: "📚 Full docs: portkey.ai/docs"
cta_discord: "💬 Join our Discord: discord.gg/DD7vgKK299"
cta_try: "🚀 Try Portkey free: app.portkey.ai"
```

---

## Content Defaults

```yaml
# SDK & Package Info
python_package: "portkey-ai"
js_package: "portkey-ai"
python_version: "3.9+"
node_version: "18+"

# Default Models (for examples)
default_provider: "openai"
default_model_openai: "gpt-4o"
default_model_anthropic: "claude-sonnet-4-20250514"
default_model_google: "gemini-2.0-flash"
default_model_mistral: "mistral-large-latest"

# Tweet settings
max_tweet_length: 280
typical_thread_length: 5-8
code_snippet_max_lines: 15

# LinkedIn settings
target_post_length: "1300-2000 characters"
max_bullet_points: 5

# Blog settings
technical_blog_length: "1500-3000 words"
coding_blog_length: "1000-2000 words"

# Hashtags
default_hashtags_twitter: "#AIGateway #LLM #Portkey #GenAI #Python"
default_hashtags_linkedin: "#AI #LLM #Portkey #ProductionAI #AIInfrastructure"

# Portkey-specific hashtags
portkey_hashtags: "#PortkeyAI #AIGateway #LLMOps #AIInfrastructure #ProductionAI"
```

---

## API Environment Variables

Content should assume these are set:

```bash
# Required
PORTKEY_API_KEY=your_portkey_api_key

# Provider Keys (used in examples)
OPENAI_API_KEY=your_openai_key
ANTHROPIC_API_KEY=your_anthropic_key
GOOGLE_API_KEY=your_google_key

# Optional
AZURE_OPENAI_API_KEY=your_azure_key
AZURE_OPENAI_ENDPOINT=your_azure_endpoint
AWS_ACCESS_KEY_ID=your_aws_key
AWS_SECRET_ACCESS_KEY=your_aws_secret
```

---

## Output Folder Structure

```
output/
├── week-1/
│   ├── cookbooks/
│   │   └── {bucket}-{title}.ipynb
│   ├── tweets/
│   │   └── {bucket}-{title}-tweet.md
│   ├── linkedin/
│   │   └── {bucket}-{title}-linkedin.md
│   ├── blogs/
│   │   ├── technical/
│   │   │   └── {bucket}-{title}-blog.md
│   │   └── coding/
│   │       └── {bucket}-{title}-tutorial.md
│   ├── snippets/
│   │   └── {bucket}-{title}-snippets.md
│   └── guides/
│       └── {language}-integration-guide.md
├── week-2/
│   └── ...
└── samples/
    └── ...
```

---

## Core Code Patterns

### Basic Portkey Setup (Python)
```python
import os
from portkey_ai import Portkey

client = Portkey(
    api_key=os.getenv("PORTKEY_API_KEY"),
    provider="openai",
    Authorization=os.getenv("OPENAI_API_KEY")
)
```

### OpenAI SDK Compatibility
```python
from openai import OpenAI
from portkey_ai import PORTKEY_GATEWAY_URL, createHeaders

client = OpenAI(
    api_key=os.getenv("OPENAI_API_KEY"),
    base_url=PORTKEY_GATEWAY_URL,
    default_headers=createHeaders(
        api_key=os.getenv("PORTKEY_API_KEY"),
        provider="openai"
    )
)
```

### Fallback Config
```python
config = {
    "strategy": {"mode": "fallback"},
    "targets": [
        {"provider": "openai", "override_params": {"model": "gpt-4o"}},
        {"provider": "anthropic", "override_params": {"model": "claude-sonnet-4-20250514"}}
    ]
}
```

### Guardrails Config
```python
config = {
    "retry": {"attempts": 3},
    "output_guardrails": [{
        "default.contains": {
            "operator": "none",
            "words": ["offensive_word"]
        },
        "deny": True
    }]
}
```

---

## Quality Checklist

Before considering content complete:

### Cookbooks
- [ ] All code cells run without errors
- [ ] Uses `portkey_ai` SDK correctly
- [ ] Shows provider switching benefit
- [ ] API keys use environment variables
- [ ] CTA with GitHub star at the end

### Tweets
- [ ] Hook stops the scroll
- [ ] Each tweet under 280 characters
- [ ] Code snippets are screenshot-ready
- [ ] Shows Portkey's 2-line integration
- [ ] CTA with docs or GitHub link

### LinkedIn
- [ ] 1300-2000 character range
- [ ] Production/enterprise narrative
- [ ] No links in main post
- [ ] Engaging question at end
- [ ] Link in first comment section

### Technical Blogs
- [ ] 1500-3000 words
- [ ] Architecture diagrams included
- [ ] Benchmark data where applicable
- [ ] Working code examples
- [ ] Links to Portkey docs

### Code Snippets
- [ ] Python, JavaScript, cURL versions
- [ ] Copy-paste ready
- [ ] Comments for key parameters
- [ ] Environment variable setup shown

---

## Tone Guidelines

### Voice
- Production-focused and pragmatic
- Developer empathy (understand the LLM ops pain)
- Data-driven (latency, cost, uptime numbers)
- Technically rigorous but accessible
- Fast-paced, value-dense

### Avoid
- Buzzword overload
- "Simply" or "just" (implies it's easy)
- Overly salesy language
- Vague claims without data
- Ignoring production concerns

### Use
- Active voice
- Concrete examples with real code
- Production scenarios and war stories
- "Here's how to..." framing
- Before/after comparisons (without Portkey vs. with Portkey)
