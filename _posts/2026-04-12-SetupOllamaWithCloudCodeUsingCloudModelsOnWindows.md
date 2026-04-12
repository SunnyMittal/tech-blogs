---
title: "Setup ollama with Cloud Code using cloud models on windows"
date: 2026-04-12
---

# Setup ollama with Cloud Code using cloud models on windows

### Install Ollama

```powershell
curl -fsSL https://ollama.com/install.sh | sh
```

### Install Claude 

```powershell
irm https://claude.ai/install.ps1 | iex
```

### Run Claude with Ollama using cloud hosted models

```powershell
ollama launch claude --model glm-5.1:cloud
ollama launch claude --model nemotron-3-super:cloud
```

## References
- https://www.youtube.com/watch?v=AKKx1PoNtnM&t=104s
- https://gist.github.com/iam-veeramalla/d0f46791619b0db348d8312060a80f2d