---
title: "Which language model performs best in Basque?"
date: 2026-05-23
draft: false
tags: ["ai", "euskara", "basque", "llm", "orai", "hitz", "benchmark", "leaderboard", "evaluation"]
---

[The Latxa model](https://www.hitz.eus/eu/node/340) was an important milestone for artificial intelligence in the Basque language. Until then, we had no open-weight model that handled Basque decently. Since then, several others have been created specifically fine-tuned for Basque: [*Kimu*](https://www.orai.eus/eu/arrakasta-kasuak/kimu-zerbitzari-propioetan-instalatzeko-euskarazko-txatbota) (Orai) and the [*Latxa Qwen3 VL*](https://huggingface.co/collections/HiTZ/latxa-vl) family of models recently released by HiTZ.

At the same time, new top-tier local models have been emerging — *Qwen*, *Gemma*, etc. — which can be especially interesting for use in agents with external tools. These models are also improving their Basque language capabilities noticeably. **But do they match the Latxa model?**

This is precisely the question I ask myself every time an interesting new model appears. Beyond running a few manual tests, it seemed necessary to build a proper ranking through a rigorous evaluation. That's how [EvalEU](https://itzune.github.io/evaleu/) was born: a project to measure and compare the Basque language proficiency of Language Models.

To this end, I have used existing Basque evaluation benchmarks and datasets (many thanks to *HiTZ* and *Orai*).

![Current ranking](/images/evaleu_table.png)
![How has it evolved over time?](/images/evaleu_timeline.png)

Among the things I would like to add in the future:

- Add automatic translation evaluations
- Beyond local models, also include large proprietary models offered via API (OpenAI, Google, Anthropic...)

The project has been published under the [Itzune](https://github.com/itzune/) initiative. In addition to the website, you will find the tools used to run the evaluations in the [repository](https://github.com/itzune/evaleu). Improvements and ideas are very welcome!
