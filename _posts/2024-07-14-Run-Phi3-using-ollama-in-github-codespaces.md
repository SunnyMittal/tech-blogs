---
title: "Run phi3 model using Ollama in github codespaces"
date: 2024-07-14
---

# Steps

1. Create a codespace using Jupyter Notebook template in Codespaces
    ![Jupyter noteBook template](/tech-blogs/assets/images/jupyterNotebookTemplateInGithubCodespaces.png)
    
2. Run below command to install ollama in codespace.

    ```curl -fsSL https://ollama.com/install.sh | sh```

3. Run below command to check if ollama is installed or not.

    ```ollama```

4. Run ollama serve to start ollama process

    ```ollama serve```

5. Open a split terminal or a new terminal and run below command to load a model and start chat session with the LLM model
    ![Starting chat session with LLM](/tech-blogs/assets/images/startingChatSesionWithPhi3LLMUsingOllama.png)