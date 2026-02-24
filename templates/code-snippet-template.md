# Code Snippet Template

Use this structure when generating standalone code snippets for Portkey AI, optimized for docs, social media, and quick reference.

---

## File Structure

```markdown
# [Feature Name] — Code Snippets

## Overview
[1-2 sentence description of what these snippets demonstrate]

---

## Python

### Installation
```bash
pip install portkey-ai
```

### Code
```python
[Python implementation]
```

---

## JavaScript / TypeScript

### Installation
```bash
npm install portkey-ai
```

### Code
```javascript
[JavaScript/TypeScript implementation]
```

---

## cURL (REST API)

```bash
[cURL command]
```

---

## Notes
[Key configuration details, gotchas, links to docs]
```

---

## Snippet Rules

1. **Self-contained**: Each snippet must run independently
2. **Copy-paste ready**: No pseudo-code or placeholders (except API keys)
3. **Commented**: Key parameters explained inline
4. **Minimal**: Show the feature, not boilerplate
5. **Consistent**: Same operation across all languages

---

## Python Snippet Pattern

```python
import os
from portkey_ai import Portkey

# Initialize Portkey client
client = Portkey(
    api_key=os.getenv("PORTKEY_API_KEY"),   # Your Portkey API key
    provider="openai",                        # LLM provider
    Authorization=os.getenv("OPENAI_API_KEY") # Provider API key
)

# Make a request through the AI Gateway
response = client.chat.completions.create(
    model="gpt-4o",
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "What is an AI Gateway?"}
    ]
)

print(response.choices[0].message.content)
```

---

## JavaScript Snippet Pattern

```javascript
import Portkey from "portkey-ai";

// Initialize Portkey client
const client = new Portkey({
  apiKey: process.env.PORTKEY_API_KEY,     // Your Portkey API key
  provider: "openai",                       // LLM provider
  Authorization: process.env.OPENAI_API_KEY // Provider API key
});

// Make a request through the AI Gateway
const response = await client.chat.completions.create({
  model: "gpt-4o",
  messages: [
    { role: "system", content: "You are a helpful assistant." },
    { role: "user", content: "What is an AI Gateway?" }
  ]
});

console.log(response.choices[0].message.content);
```

---

## cURL Snippet Pattern

```bash
curl https://api.portkey.ai/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "x-portkey-api-key: $PORTKEY_API_KEY" \
  -H "x-portkey-provider: openai" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "gpt-4o",
    "messages": [
      {"role": "system", "content": "You are a helpful assistant."},
      {"role": "user", "content": "What is an AI Gateway?"}
    ]
  }'
```

---

## Advanced Snippet Patterns

### Fallback (Python)
```python
config = {
    "strategy": {"mode": "fallback"},
    "targets": [
        {"provider": "openai", "override_params": {"model": "gpt-4o"}},
        {"provider": "anthropic", "override_params": {"model": "claude-sonnet-4-20250514"}}
    ]
}

client = client.with_options(config=config)
response = client.chat.completions.create(
    messages=[{"role": "user", "content": "Hello!"}]
)
```

### Guardrails (Python)
```python
config = {
    "retry": {"attempts": 3},
    "output_guardrails": [{
        "default.contains": {
            "operator": "none",
            "words": ["sensitive_word"]
        },
        "deny": True
    }]
}

client = client.with_options(config=config)
```

### Streaming (Python)
```python
stream = client.chat.completions.create(
    model="gpt-4o",
    messages=[{"role": "user", "content": "Tell me a story"}],
    stream=True
)

for chunk in stream:
    if chunk.choices[0].delta.content:
        print(chunk.choices[0].delta.content, end="")
```

### Prompt Management (Python)
```python
# Execute a prompt saved in Portkey's Prompt Library
response = client.prompts.completions.create(
    prompt_id="pp-my-prompt-id",
    variables={
        "topic": "AI Gateways"
    }
)

print(response.choices[0].message.content)
```

### Observability / Metadata (Python)
```python
# Tag request with metadata for observability
client = client.with_options(
    metadata={
        "_user": "user_123",
        "environment": "production",
        "session_id": "sess_abc"
    }
)

response = client.chat.completions.create(
    model="gpt-4o",
    messages=[{"role": "user", "content": "Hello!"}]
)
```

### OpenAI SDK Compatibility (Python)
```python
from openai import OpenAI
from portkey_ai import PORTKEY_GATEWAY_URL, createHeaders

# Use your existing OpenAI code — just change 2 lines
client = OpenAI(
    api_key=os.getenv("OPENAI_API_KEY"),
    base_url=PORTKEY_GATEWAY_URL,           # ← Line 1
    default_headers=createHeaders(           # ← Line 2
        api_key=os.getenv("PORTKEY_API_KEY"),
        provider="openai"
    )
)

# Everything else stays the same!
response = client.chat.completions.create(
    model="gpt-4o",
    messages=[{"role": "user", "content": "Hello!"}]
)
```

---

## File Naming

Format: `{bucket}-{short-title}-snippets.md`

Examples:
- `gateway-basic-setup-snippets.md`
- `gateway-fallback-config-snippets.md`
- `guardrails-output-validation-snippets.md`
- `observability-metadata-logging-snippets.md`
- `prompt-management-execution-snippets.md`
