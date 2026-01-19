---
category: Node.js
path: '/api/chat'
title: 'Fetch streaming chat response'
type: 'POST'
layout: null
---

This method allows users to send messages and receive streaming AI responses.

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

### Node.js Example
```javascript
#!/usr/bin/env node
const fetch = require('node-fetch');

async function testChat(message) {
  console.log(`Testing: ${message}`);

  try {
    const response = await fetch('https://ai.callaback.workers.dev/api/chat', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        messages: [{ role: 'user', content: message }]
      })
    });

    const reader = response.body.getReader();
    const decoder = new TextDecoder();
    let buffer = '';
    let fullResponse = '';

    while (true) {
      const { done, value } = await reader.read();
      if (done) break;

      buffer += decoder.decode(value, { stream: true });
      const lines = buffer.split('\n');
      buffer = lines.pop() || '';

      for (const line of lines) {
        if (line.startsWith('data: ')) {
          const data = line.slice(6);
          if (data === '[DONE]') {
            console.log('\n✓');
            return fullResponse;
          }

          // Try to parse as JSON
          try {
            const parsed = JSON.parse(data);
            if (parsed.response) {
              process.stdout.write(parsed.response);
              fullResponse += parsed.response;
            }
          } catch (e) {
            // If not JSON, try regex extraction
            const match = data.match(/"response":"([^"]*)"/);
            if (match && match[1]) {
              process.stdout.write(match[1]);
              fullResponse += match[1];
            }
          }
        }
      }
    }
  } catch (error) {
    console.error(`Error: ${error.message}`);
  }
}

async function runTests() {
  const tests = [
    "Hello",
    "What is 2+2?",
    "Tell me a joke"
  ];

  for (const test of tests) {
    await testChat(test);
  }
}

runTests();
```

### Usage
```bash
node testApi.js
```

For error responses, see the [response status codes documentation](#response-status-codes).
