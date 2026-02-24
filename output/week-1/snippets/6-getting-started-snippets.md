# Portkey AI — Essential Code Snippets

## Overview
These essential snippets demonstrate how to perform core LLM operations (basic setup, chat completions, streaming, and embeddings) through Portkey's AI Gateway using Python, JavaScript, and cURL. 

Portkey routing helps you manage over 250+ LLMs with enterprise-grade reliability. Remember to replace placeholder API keys with your actual keys.

---

## Python

### Installation
```bash
pip install portkey-ai
```

### Basic Setup & Chat Completions
```python
import os
from portkey_ai import Portkey

# Initialize Portkey client
client = Portkey(
    api_key=os.getenv("PORTKEY_API_KEY"),   # Your Portkey API key
    provider="openai",                        # LLM provider (e.g., openai, anthropic, google)
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

### Streaming
```python
# Stream responses token-by-token
stream = client.chat.completions.create(
    model="gpt-4o",
    messages=[{"role": "user", "content": "Write a short poem about production AI."}],
    stream=True
)

for chunk in stream:
    if chunk.choices[0].delta.content:
        print(chunk.choices[0].delta.content, end="")
```

### Embeddings
```python
# Generate vector embeddings
response = client.embeddings.create(
    input="Portkey is an AI Gateway for production.",
    model="text-embedding-3-small"
)

print(f"Embedding dimensions: {len(response.data[0].embedding)}")
```

---

## JavaScript / TypeScript

### Installation
```bash
npm install portkey-ai
```

### Basic Setup & Chat Completions
```javascript
import Portkey from "portkey-ai";

// Initialize Portkey client
const client = new Portkey({
  apiKey: process.env.PORTKEY_API_KEY,      // Your Portkey API key
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

### Streaming
```javascript
// Stream responses token-by-token
const stream = await client.chat.completions.create({
  model: "gpt-4o",
  messages: [{ role: "user", content: "Write a short poem about production AI." }],
  stream: true
});

for await (const chunk of stream) {
  if (chunk.choices[0].delta.content) {
    process.stdout.write(chunk.choices[0].delta.content);
  }
}
```

### Embeddings
```javascript
// Generate vector embeddings
const response = await client.embeddings.create({
  input: "Portkey is an AI Gateway for production.",
  model: "text-embedding-3-small"
});

console.log(`Embedding dimensions: ${response.data[0].embedding.length}`);
```

---

## cURL (REST API)

### Basic Setup & Chat Completions
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

### Streaming
```bash
curl https://api.portkey.ai/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "x-portkey-api-key: $PORTKEY_API_KEY" \
  -H "x-portkey-provider: openai" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "gpt-4o",
    "stream": true,
    "messages": [
      {"role": "user", "content": "Write a short poem about production AI."}
    ]
  }'
```

### Embeddings
```bash
curl https://api.portkey.ai/v1/embeddings \
  -H "Content-Type: application/json" \
  -H "x-portkey-api-key: $PORTKEY_API_KEY" \
  -H "x-portkey-provider: openai" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "input": "Portkey is an AI Gateway for production.",
    "model": "text-embedding-3-small"
  }'
```

---

## Notes
- **Providers:** You can switch `openai` with `anthropic`, `google`, `cohere`, etc. Just change the `provider` property and pass the corresponding `Authorization` key.
- **Compatibility:** Portkey fully supports the OpenAI SDK. If you are using the official OpenAI client, you can just change the `base_url` and inject Portkey headers to get full gateway capabilities.
- **Documentation:** Explore advanced capabilities like Fallbacks, Rate Limiting, and Guardrails in the [Portkey Documentation](https://portkey.ai/docs).
