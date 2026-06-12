---
title: "Setup Claude To Call Gemini LLM"
date: 2026-06-02
---

# Setup Claude To Call Gemini LLM

### Install Claude if its not already done

```powershell
curl -fsSL https://ollama.com/install.sh | sh
```

### Generate Gemini pro api key
Navigate to [Google AI Studio](https://aistudio.google.com/api-keys)

Click Create API Key button to generate one.

### Set Gemini api key

```powershell
[Environment]::SetEnvironmentVariable("GEMINI_API_KEY", "<api key Value>", "User")
```

### Create Gemini gateway on local that will forward claude requests to Gemini LLM models 

Steps

1. Create a new folder and initialize
    - Open PowerShell.
    - mkdir C:\ai-gateway && cd C:\ai-gateway
    - npm init -y
2. Install a lightweight gateway package (example implementation)
    - npm install express
3. Create gateway server file
    - Create C:\ai-gateway\server.js with this content:

```powershell
const express = require('express');
const app = express();
app.use(express.json());

const GEMINI_KEY = process.env.GEMINI_API_KEY;
if (!GEMINI_KEY) { console.error('Set GEMINI_API_KEY'); process.exit(1); }

app.post('/v1/complete', async (req, res) => {
  try {
    const r = await fetch(
      `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash:generateContent?key=${GEMINI_KEY}`,
      {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
          contents: [{ parts: [{ text: req.body.prompt ?? req.body.input ?? '' }] }],
          generationConfig: {
            temperature: req.body.temperature ?? 0.2,
            maxOutputTokens: req.body.max_tokens ?? 512
          }
        })
      }
    );
    const json = await r.json();
    const text = json?.candidates?.[0]?.content?.parts?.[0]?.text ?? JSON.stringify(json);
    res.json({ completion: text, raw: json });
  } catch (e) {
    res.status(500).json({ error: String(e) });
  }
});

app.listen(3000, () => console.log('Gateway listening on http://localhost:3000'));
```

### Run Gemini gateway

```powershell
PS D:\AI\gemini-gateway> node .\server.js
```

### Test Gemini gateway

```powershell
[System.IO.File]::WriteAllText("$env:TEMP\body.json", '{"prompt":"Say hello","max_tokens":20}')
curl.exe -X POST http://localhost:3000/v1/complete -H "Content-Type: application/json" -d "@$env:TEMP\body.json"
```

Sample response:
```powershell
{"completion":"Hello!","raw":{"candidates":[{"content":{"parts":[{"text":"Hello!"}],"role":"model"},"finishReason":"STOP","index":0}],"usageMetadata":{"promptTokenCount":2,"candidatesTokenCount":2,"totalTokenCount":25,"promptTokensDetails":[{"modality":"TEXT","tokenCount":2}],"thoughtsTokenCount":21,"serviceTier":"standard"},"modelVersion":"gemini-2.5-flash","responseId":"9s4earWGJfiMjuMPhtXHiQs"}}
```

### Point claude code to Gemini gateway

```powershell
$Env:ANTHROPIC_BASE_URL="http://localhost:3000"
```

![App settings](/tech-blogs/assets/images/callGeminiFromClaudeDesktopViaGateway.png)

## References
- query to [DuckDuckGo AI](https://duck.ai/chat) - `launch claude with gemini on windows machine using gateway approach`