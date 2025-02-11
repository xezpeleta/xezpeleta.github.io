---
title: "Local RAG in Basque using Tulu-3"
date: 2024-02-14
draft: false
tags: ["llm", "rag", "basque", "ai", "tulu", "ollama"]
---

In recent months, Local LLMs have significantly improved, and some of them perform surprisingly well with Basque language. Among them, I want to highlight [Tulu-3](https://allenai.org/blog/tulu-3-technical) 70B, which shows good results in Basque when using the quantized version (q4_K_M). Until the Latxa instruction model becomes available, this is probably the best option for having conversations or generating text in Basque.

![Conversation in basque with Tulu3 model, using Open-WebUI](/images/openwebui_chat.png)

![An external resource has been used to answer a question, using RAG](/images/openwebui_citation.png)

## Components for setting up the RAG system

The components needed to set up a RAG (Retrieval Augmented Generation) system:

1. **Local LLM**: Tulu-3 70B q4_K_M
2. **Embedding model**: [Snowflake/snowflake-arctic-embed-l-v2.0](https://huggingface.co/Snowflake/snowflake-arctic-embed-l-v2.0)
3. **User interface**: [Open-WebUI](https://github.com/open-webui/open-webui)
4. **Ollama**: For managing LLMs and embedding models

## Advantages

The main advantages of this system:

- **Privacy**: Everything runs locally, data stays on your machine
- **Basque support**: Tulu-3 model performs well with Basque language
- **Free**: All components used are open source and free
- **Easy**: Thanks to Open-WebUI, everything can be managed from a graphical interface

I will update this article when the Latxa instruction model is released, but for now, Tulu-3 is an excellent choice for setting up a RAG system in Basque.