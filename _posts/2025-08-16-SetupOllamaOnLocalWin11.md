---
title: "Setup Ollama with VS Code using Continue extension on localhost in Windows 11"
date: 2025-08-16
---

# This article describes how to setup Ollama with VS Code using Continue extension on localhost in windows 11

> Steps:
1. Download ollamaSetup.exe from https://ollama.com/download
    Setup system environment variable as below. This will keep place the downloaded model in a specified folder.
    ```
    OLLAMA_MODELS = D:\AI\Models
    ```
2. Pull Qwen/Qwen2.5-Coder-32B-Instruct model using below command
    ```
    ollama pull codellama:34b-instruct
    ```
3. Start serving the model
    ```
    ollama serve
    ```
    If this step give error saying port is already being listened to then that mean ollama process is already running
    Then we can run a specific model by checking available models using this command ``` ollama list ```
    Once we know the model to run execute this command to run that specific model <b> from the project directory </b> ```ollama run codellama:34b-instruct```
4. Create environment variables (Optional)
    ```
    # Custom Ollama server
    REM From cmd prompt execute below command to set the environment variable
    SET OLLAMA_BASE_URL="http://localhost:11434/v1"
    SET OLLAMA_MODEL="codellama:34b-instruct"
    REM test if the value is set using below command
    echo %OLLAMA_MODEL%
    ```
5. Install Continue.dev extension in VS Code
6. Configure Continue extension with local model
    Config file location: C:\Users\sunny\.continue\config.yaml
    ```
    name: Local Assistant
    version: 1.0.0
    schema: v1
    models:
    - name: Chat/Edit/Apply codellama:34b-instruct
        provider: ollama
        model: codellama:34b-instruct
        roles:
        - chat
        - edit
        - apply
    - name: Autocomplete codellama:34b-instruct
        provider: ollama
        model: codellama:34b-instruct
        roles:
        - autocomplete
    - name: Embed codellama:34b-instruct
        provider: ollama
        model: codellama:34b-instruct
        roles:
        - embed
    context:
    - provider: code
    - provider: docs
    - provider: diff
    - provider: terminal
    - provider: problems
    - provider: folder
    - provider: codebase
    ```
7. Use Continue extension in offline mode and it works

## References
- https://ollama.com/download
- https://ollama.com/blog/continue-code-assistant