---
title: "Setup MCP Client using python"
date: 2025-09-20
---

# This article describes how to setup MCP client using python

Steps:
### Create project directory
>`uv init mcp-client`

>`cd mcp-client`

### Create virtual environment
`uv venv`

### Activate virtual environment
On Windows:
>`.venv\Scripts\activate`

On Unix or macOS:
>`source .venv/bin/activate`

### Install required packages
`uv add mcp anthropic python-dotenv`

### Remove boilerplate files
On Windows:
>`del main.py`

On Unix or macOS:
>`rm main.py`

### Create our main file
On Windows:
>`New-Item client.py -ItemType File`

On Unix or macOS:
>`touch client.py`

## References
- https://modelcontextprotocol.io/docs/develop/build-client