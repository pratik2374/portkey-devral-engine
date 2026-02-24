# Portkey AI Integration Guide: Python

## Quick Start

The fastest way to route your first request through Portkey's AI Gateway.

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

That's it! Your request is now routed through Portkey, fully visible in your observability dashboard.

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

There are two primary ways to authenticate and route requests through Portkey using Python. 

### Option 1: Portkey Native SDK (Recommended)
This method allows you to instantly switch providers by simply changing the `provider` parameter.

```python
from portkey_ai import Portkey

client = Portkey(
    # Your Portkey workspace key
    api_key=os.getenv("PORTKEY_API_KEY"),
    
    # The provider you want Portkey to route this client's requests to
    provider="openai",
    
    # The provider's API key
    Authorization=os.getenv("OPENAI_API_KEY"),
    
    # Optional: Send requests to a specific workspace if you have multiple
    # workspace_id="ws-uuid-here"
)
```

### Option 2: OpenAI SDK Compatibility
If you have an existing codebase built entirely utilizing the official `openai` Python SDK, you can route all traffic through Portkey by changing only two lines of code during client initialization:

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

Once your client is initialized, executing operations feels identical to standard provider SDKs.

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
To receive responses token-by-token, set `stream=True`.

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

## Advanced Features

Portkey's true power lies in its Gateway configurations. You append these configurations to your client using the `.with_options()` method.

### Fallbacks
Route a request to a secondary provider instantly if the primary fails.

```python
config = {
    "strategy": {"mode": "fallback"},
    "targets": [
        {"provider": "openai", "override_params": {"model": "gpt-4o"}},
        {"provider": "anthropic", "override_params": {"model": "claude-3-5-sonnet-20241022"}}
    ]
}

secure_client = client.with_options(config=config)
```

### Load Balancing
Distribute traffic evenly across multiple API keys to multiply your rate limits.

```python
config = {
    "strategy": {"mode": "loadbalance"},
    "targets": [
        {"provider": "openai", "weight": 0.5, "api_key": "openai-key-1"},
        {"provider": "openai", "weight": 0.5, "api_key": "openai-key-2"}
    ]
}

load_balanced_client = client.with_options(config=config)
```

### Semantic Caching
Save up to 40% on API costs by returning cached responses for mathematically similar prompts.

```python
config = {
    "cache": {"mode": "semantic", "max_age": 3600}
}

fast_client = client.with_options(config=config)
```

### Guardrails
Block unsafe inputs or outputs before they break your app using 50+ pre-built checks (e.g., PII redaction, toxicity).

```python
config = {
    "output_guardrails": [{
        "default.contains": {
            "operator": "none",
            "words": ["restricted_competitor_name"]
        },
        "deny": True
    }],
    "retry": {"attempts": 3}
}

guarded_client = client.with_options(config=config)
```

### Prompt Management
Stop hardcoding prompts. Version and execute them directly from Portkey's Cloud Library.

```python
response = client.prompts.completions.create(
    prompt_id="pp-my-production-prompt",
    variables={"target_audience": "enterprise developers"}
)
print(response.choices[0].message.content)
```

### Observability Metadata
Tag requests to segment your dashboard analytics by tenant or feature.

```python
traced_client = client.with_options(
    metadata={
        "_environment": "production",
        "_user": "tenant_1092",
        "feature": "invoice_extraction"
    },
    trace_id="document_run_55"
)
```

## Framework Integration

Portkey integrates cleanly into Python's most popular synchronous and asynchronous web frameworks.

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
from django.http import JsonResponse
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

## Idiomatic Error Handling

Handle Portkey exceptions cleanly to implement custom application-level fallback logic if needed.

```python
from portkey_ai import Portkey
from portkey_ai.exceptions import (
    AuthenticationError,
    NotFoundError,
    RateLimitError,
    APIError
)

try:
    response = client.chat.completions.create(
        model="gpt-4o",
        messages=[{"role": "user", "content": "Hello!"}]
    )
except AuthenticationError:
    print("Authentication failed. Check your PORTKEY_API_KEY and provider API key.")
except NotFoundError:
    print("The requested model or resource does not exist.")
except RateLimitError:
    print("Provider rate limit reached. Consider adding Load Balancing to your Portkey config.")
except APIError as e:
    print(f"A generalized API error occurred: {e}")
```

## Reference

- [Portkey API Reference & Postman Collection](https://portkey.ai/docs/api-reference)
- [Official Quickstart Documentation](https://portkey.ai/docs/welcome/make-your-first-request)
- [Managing Virtual Keys for Authentication](https://portkey.ai/docs/product/ai-gateway/virtual-keys)
