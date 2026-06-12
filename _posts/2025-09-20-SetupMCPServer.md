---
title: "Setup MCP Server using python"
date: 2025-09-21
---

# This article describes how to setup MCP server using python

Steps:
### Create a new directory for our project
```uv init weather
cd weather
```

### Create virtual environment and activate it
```
uv venv
.venv\Scripts\activate
```

### Install dependencies
```uv add mcp[cli] httpx```

### Create our server file
```new-item weather.py```


## References
- https://modelcontextprotocol.io/docs/develop/build-server#python