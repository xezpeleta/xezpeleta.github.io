---
title: "RAG lokala euskaraz Tülu 3 erabiliz"
date: 2024-02-14
draft: false
tags: ["llm", "rag", "euskara", "ai", "tulu", "ollama"]
---

Azken hilabeteetan LLM eredu lokal eta *askeak* asko hobetu dira, eta horietako batzuk euskaraz ere nahiko ondo moldatzen dira. Horien artean, [Tülu-3](https://allenai.org/blog/tulu-3-technical) 70B nabarmendu nahi nuke, kuantizatutako bertsioa erabilita (q4_K_M) euskaraz emaitza onak ematen baititu. Latxa chat edo instrukzio eredua argitaratu arte, ziurrenik aukera onena da euskarazko elkarrizketak izateko edo testuak sortzeko.

![Open-WebUI bidezko elkarrizketa, Tulu3 ereduarekin](/images/openwebui_chat.png)

![Galderari erantzuteko, RAG bidez erabilitako kanpo baliabideak](/images/openwebui_citation.png)


## RAG sistema martxan jartzeko osagaiak

RAG (Retrieval Augmented Generation) sistema bat martxan jartzeko behar ditugun osagaiak:

1. **LLM lokala**: Tülu-3 70B q4_K_M
2. **Embedding modeloa**: [Snowflake/snowflake-arctic-embed-l-v2.0](https://huggingface.co/Snowflake/snowflake-arctic-embed-l-v2.0)
3. **Erabiltzaile interfazea**: [Open-WebUI](https://github.com/open-webui/open-webui)
4. **Ollama**: LLM-ak eta embedding modeloak kudeatzeko

## Abantailak

Sistema honen abantaila nagusiak:

- **Pribatutasuna**: Dena lokalean exekutatzen da, datuak zure ekipoan geratzen dira
- **Euskara**: Tulu-3 modeloak euskaraz nahiko ondo funtzionatzen du
- **Doakoa**: Erabilitako osagai guztiak kode irekikoak eta doakoak dira
- **Erraza**: Open-WebUI-ri esker, interfaze grafiko batetik kudeatu daiteke dena

Latxa instruction eredua argitaratzen denean eguneratuko dut artikulua, baina momentuz Tülu-3 aukera bikaina da euskarazko RAG sistema bat martxan jartzeko.