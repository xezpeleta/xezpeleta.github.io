---
title: "Kimu"
date: 2024-10-13
draft: false
tags: ["llm", "orai", "basque", "ai", "gemma", "llama.cpp", "ollama"]
cover:
    image: "/images/kimu-cover.png"
    alt: "Kimu eredua"
    caption: "AI generated image"
---

[Orai](https://www.orai.eus/) has just released a language model called [Kimu](https://www.orai.eus/eu/bloga/zerbitzari-propioetan-instalatzeko-moduko-euskarazko-txatbot-berria-kimu).

Based on [Gemma 2](https://developers.googleblog.com/es/gemma-explained-new-in-gemma-2/), they have created models with 2B and 9B parameters. They have successfully injected the knowledge required to speak and understand Basque into the base model.

I have converted both Kimu models to the GGUF format and [published them on Hugging Face](https://huggingface.co/collections/itzune/kimu-68eba95715355bbb972c32f8). This makes it possible to use the Kimu model with applications like Llama.cpp or Ollama.

![Kimu models in the Hugging Face repository](/images/hf_itzune_kimu.png)

At the same time, [@urtzai](https://mastodon.eus/@urtzai) has published these models in the [Ollama model catalog](https://ollama.com/itzune/kimu), making them even easier to use via Ollama.

Just install Ollama, and by running the following command you can get it up and running:

```bash
ollama run itzune/kimu:2b
```

![Kimu models in the Ollama catalog](/images/ollama_itzune_kimu.png)

> An important step by Orai; we finally have a small and lightweight model that performs well in Basque.

An essential step to ensure Basque does not fall behind in the LLM application space!

![First tests with the Kimu 2B model](/images/kimu_test.png)


