---
title: "Kimu"
date: 2024-10-13
draft: false
tags: ["llm", "orai", "basque", "ai", "gemma", "llama.cpp", "ollama"]
---

Kimu izeneko hizkuntza eredua [argitaratu berri du](https://www.orai.eus/eu/bloga/zerbitzari-propioetan-instalatzeko-moduko-euskarazko-txatbot-berria-kimu) Orai-k.

Gemma 2 ereduan oinarrituta,  2B eta 9B parametro dituzten ereduak sortu dituzte. Oinarrizko ereduari euskaraz egiteko beharrezko jakintza txertatzea lortu dute.

Kimu-ko bi ereduak GGUF formatura bihurtu ditut eta [Hugging Face biltegian jarri ditut eskuragarri](https://huggingface.co/collections/itzune/kimu-68eba95715355bbb972c32f8). Modu honetara, Kimu eredua Llama.cpp edo Ollama bezalako aplikazioetan erabiltzea posible da.

![Kimu ereduak Hugging Face biltegian](/images/hf_itzune_kimu.png)

Aldi berean, @urtzai-k eredu hauek [Ollama-ko eredu katalogoan](https://ollama.com/itzune/kimu) argitaratu ditu, Ollama bidez erabilera errazagoa eginez:

Ollama instalatu, eta honako agindu hau exekutatuz,

```bash
ollama run itzune/kimu:2b
```

![Kimu ereduak Ollama biltegian](/images/ollama_itzune_kimu.png)

> Urrats garrantzitsua Orai-k eman duena; azkenean badugu euskaraz ongi egiten duen eredu txiki eta arina.

LLM-en aplikazioen esparruan euskara atzean ez gelditzeko ezinbestekoa.