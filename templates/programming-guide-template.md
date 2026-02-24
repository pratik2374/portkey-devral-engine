# Programming Language Guide Template

Use this structure when generating language-specific integration guides for Portkey AI.

---

## File Structure

```markdown
# Portkey AI Integration Guide: [Language]

## Quick Start
[Fastest path to first API call — under 2 minutes]

## Installation
[Package manager setup for the language]

## Authentication
[API key configuration patterns]

## Core Operations
### Chat Completions
### Streaming
### Embeddings
### Image Generation

## Advanced Features
### Fallbacks
### Load Balancing
### Caching
### Guardrails
### Prompt Management
### Observability

## Framework Integration
[Language-specific web framework examples]

## Error Handling
[Idiomatic error handling patterns]

## Migration from Direct Provider SDK
[How to switch from OpenAI/Anthropic SDK to Portkey]

## Reference
[Links to API docs, SDK docs, examples]
```

---

## Supported Languages

Create guides for:
1. **Python** — Primary language, most comprehensive
2. **JavaScript / TypeScript** — Node.js and edge runtimes
3. **Go** — For backend/infrastructure teams
4. **cURL / REST** — Universal, works everywhere

---

## Python Guide Pattern

```markdown
# Portkey AI Integration Guide: Python

## Quick Start

```bash
pip install portkey-ai
```

```python
import os
from portkey_ai import Portkey

client = Portkey(
    api_key=os.getenv("PORTKEY_API_KEY"),
    provider="openai",
    Authorization=os.getenv("OPENAI_API_KEY")
)

response = client.chat.completions.create(
    model="gpt-4o",
    messages=[{"role": "user", "content": "Hello from Portkey!"}]
)
print(response.choices[0].message.content)
```

That's it! Your request is now routed through Portkey's AI Gateway.

## Installation

```bash
# Recommended: use a virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install Portkey SDK
pip install portkey-ai

# Optional: for OpenAI compatibility mode
pip install openai
```

**Requirements**: Python 3.9+

## Authentication

### Option 1: Portkey SDK (Recommended)
```python
from portkey_ai import Portkey

client = Portkey(
    api_key=os.getenv("PORTKEY_API_KEY"),
    provider="openai",
    Authorization=os.getenv("OPENAI_API_KEY")
)
```

### Option 2: OpenAI SDK Compatibility
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

## Core Operations

### Chat Completions
```python
response = client.chat.completions.create(
    model="gpt-4o",
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "Explain AI Gateways in 2 sentences."}
    ],
    temperature=0.7,
    max_tokens=150
)
print(response.choices[0].message.content)
```

### Streaming
```python
stream = client.chat.completions.create(
    model="gpt-4o",
    messages=[{"role": "user", "content": "Tell me a story"}],
    stream=True
)

for chunk in stream:
    if chunk.choices[0].delta.content:
        print(chunk.choices[0].delta.content, end="", flush=True)
```

### Embeddings
```python
response = client.embeddings.create(
    model="text-embedding-3-small",
    input="What is an AI Gateway?"
)
print(f"Embedding dimension: {len(response.data[0].embedding)}")
```

### Image Generation
```python
response = client.images.generate(
    model="dall-e-3",
    prompt="A futuristic AI gateway in space, cyberpunk style",
    n=1,
    size="1024x1024"
)
print(f"Generated Image URL: {response.data[0].url}")
```

## Advanced Features

### Fallbacks
```python
config = {
    "strategy": {"mode": "fallback"},
    "targets": [
        {"provider": "openai", "override_params": {"model": "gpt-4o"}},
        {"provider": "anthropic", "override_params": {"model": "claude-sonnet-4-20250514"}}
    ]
}
client = client.with_options(config=config)
```

### Load Balancing
```python
config = {
    "strategy": {"mode": "loadbalance"},
    "targets": [
        {"provider": "openai", "weight": 0.5, "api_key": "openai-key-1"},
        {"provider": "openai", "weight": 0.5, "api_key": "openai-key-2"}
    ]
}
client = client.with_options(config=config)
```

### Caching
```python
config = {
    "cache": {"mode": "semantic", "max_age": 3600}
}
client = client.with_options(config=config)
```

### Guardrails
```python
config = {
    "output_guardrails": [{
        "default.contains": {
            "operator": "none",
            "words": ["restricted_word"]
        },
        "deny": True
    }],
    "retry": {"attempts": 3}
}
client = client.with_options(config=config)
```

### Prompt Management
```python
response = client.prompts.completions.create(
    prompt_id="pp-my-prompt-id",
    variables={"user_name": "Alice"}
)
print(response.choices[0].message.content)
```

### Observability
```python
client = client.with_options(
    metadata={"user_id": "user-123", "org": "acme-corp"}
)
response = client.chat.completions.create(
    model="gpt-4o",
    messages=[{"role": "user", "content": "Hello!"}]
)
```

## Framework Integration

### FastAPI
```python
from fastapi import FastAPI
from portkey_ai import Portkey

app = FastAPI()
client = Portkey(
    api_key=os.getenv("PORTKEY_API_KEY"),
    provider="openai",
    Authorization=os.getenv("OPENAI_API_KEY")
)

@app.post("/chat")
async def chat(message: str):
    response = client.chat.completions.create(
        model="gpt-4o",
        messages=[{"role": "user", "content": message}]
    )
    return {"response": response.choices[0].message.content}
```

### Django
```python
# views.py
from portkey_ai import Portkey

client = Portkey(
    api_key=os.getenv("PORTKEY_API_KEY"),
    provider="openai",
    Authorization=os.getenv("OPENAI_API_KEY")
)

def chat_view(request):
    message = request.POST.get("message")
    response = client.chat.completions.create(
        model="gpt-4o",
        messages=[{"role": "user", "content": message}]
    )
    return JsonResponse({"response": response.choices[0].message.content})
```

## Error Handling

```python
from portkey_ai import Portkey
from portkey_ai.exceptions import (
    AuthenticationError,
    RateLimitError,
    APIError
)

try:
    response = client.chat.completions.create(
        model="gpt-4o",
        messages=[{"role": "user", "content": "Hello!"}]
    )
except AuthenticationError:
    print("Check your PORTKEY_API_KEY and provider API key")
except RateLimitError:
    print("Rate limited — consider adding load balancing config")
except APIError as e:
    print(f"API error: {e}")
```

## Migration from OpenAI SDK

```diff
- from openai import OpenAI
+ from portkey_ai import Portkey

- client = OpenAI(api_key=os.getenv("OPENAI_API_KEY"))
+ client = Portkey(
+     api_key=os.getenv("PORTKEY_API_KEY"),
+     provider="openai",
+     Authorization=os.getenv("OPENAI_API_KEY")
+ )

# Everything below stays exactly the same!
response = client.chat.completions.create(
    model="gpt-4o",
    messages=[{"role": "user", "content": "Hello!"}]
)
```
```

---

## JavaScript / TypeScript Guide Pattern

```markdown
# Portkey AI Integration Guide: JavaScript / TypeScript

## Quick Start

```bash
npm install portkey-ai
```

```typescript
import Portkey from "portkey-ai";

const client = new Portkey({
  apiKey: process.env.PORTKEY_API_KEY,
  provider: "openai",
  Authorization: process.env.OPENAI_API_KEY,
});

const response = await client.chat.completions.create({
  model: "gpt-4o",
  messages: [{ role: "user", content: "Hello from Portkey!" }],
});

console.log(response.choices[0].message.content);
```

## Framework Integration

### Express.js
```typescript
import express from "express";
import Portkey from "portkey-ai";

const app = express();
const client = new Portkey({
  apiKey: process.env.PORTKEY_API_KEY,
  provider: "openai",
  Authorization: process.env.OPENAI_API_KEY,
});

app.post("/chat", async (req, res) => {
  const response = await client.chat.completions.create({
    model: "gpt-4o",
    messages: [{ role: "user", content: req.body.message }],
  });
  res.json({ response: response.choices[0].message.content });
});
```

### Next.js (API Route)
```typescript
// app/api/chat/route.ts
import Portkey from "portkey-ai";
import { NextResponse } from "next/server";

const client = new Portkey({
  apiKey: process.env.PORTKEY_API_KEY,
  provider: "openai",
  Authorization: process.env.OPENAI_API_KEY,
});

export async function POST(request: Request) {
  const { message } = await request.json();
  const response = await client.chat.completions.create({
    model: "gpt-4o",
    messages: [{ role: "user", content: message }],
  });
  return NextResponse.json({ response: response.choices[0].message.content });
}
```
```

---

## File Naming

Format: `{language}-integration-guide.md`

Examples:
- `python-integration-guide.md`
- `javascript-integration-guide.md`
- `go-integration-guide.md`
- `rest-api-guide.md`
