---
category: Python
path: '/api/chat'
title: 'POST streaming chat with requests'
type: 'POST'
layout: null
---

This method allows users to send messages via Python's `requests` library and receive streaming AI responses.

### Request

* **Endpoint:** `https://ai.callaback.workers.dev/api/chat`
* **Method:** `POST`
* **Headers:** `Content-Type: application/json`
* **Body:**
```json
{
  "messages": [
    { "role": "user", "content": "Your message here" }
  ]
}
```

### Response

Returns a streaming response with Server-Sent Events (SSE).

**Status:** `200 OK`

**Stream format:**
```
data: {"response":"Hello"}
data: {"response":" there"}
data: [DONE]
```

### Python Client Example
```python
import requests
import json
import re

def stream_chat(messages):
    url = "https://ai.callaback.workers.dev/api/chat"
    response = requests.post(url, json={"messages": messages}, stream=True)
    
    for line in response.iter_lines():
        if line:
            line = line.decode('utf-8')
            if line.startswith('data: '):
                data = line[6:]
                if data == '[DONE]':
                    break
                # Parse response chunk
                match = re.search(r'"response":"([^"]*)"', data)
                if match:
                    yield match.group(1)

# Usage
for chunk in stream_chat([{"role": "user", "content": "Hello"}]):
    print(chunk, end='', flush=True)
```

### Multi-turn Conversation
```python
# Continue the conversation
messages = [
    {"role": "user", "content": "Hello"},
    {"role": "assistant", "content": "Hi! How can I help you?"},
    {"role": "user", "content": "What is 2+2?"}
]

for chunk in stream_chat(messages):
    print(chunk, end='', flush=True)
print()  # New line after response
```

### Installation
```bash
pip install requests
```

### Usage
```bash
python chat_client.py
```

### Response Processing

The client handles streaming by:
- Setting `stream=True` in the request
- Iterating through lines with `iter_lines()`
- Parsing SSE format with `data:` prefix
- Extracting JSON response fields with regex
- Yielding chunks for real-time display

For error responses, see the [response status codes documentation](#response-status-codes).
