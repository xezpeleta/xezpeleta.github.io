---
title: "Zein hizkuntza eredu da hobea euskaraz?"
date: 2026-05-23
draft: false
tags: ["ai", "euskara", "llm", "orai", "hitz", "benchmark", "leaderboard", "evaluation"]
---

[Latxa eredua](https://www.hitz.eus/eu/node/340) mugarri garrantzitsu bat izan zen euskarazko adimen artifizialrentzat. Ordurarte ez genuen euskaraz txukun egiten zuen pisu irekiko eredurik. Ondorenera bereziki euskaraz fin egiteko diseinatuak izan diren beste batzuk sortu dira: [*Kimu*](https://www.orai.eus/eu/arrakasta-kasuak/kimu-zerbitzari-propioetan-instalatzeko-euskarazko-txatbota) (Orai) edota Hitz-ek duela gutxi argitaratutako [*Latxa Qwen3 VL*](https://huggingface.co/collections/HiTZ/latxa-vl) familiako ereduak.

Aldi berean, lehen mailako eredu lokal berriak agertzen joan dira: *Qwen*, *Gemma*, etab. Bereziki interesgarriak izan daitezkeenak agenteetan kanpo-tresnak erabiltzeko. Hauek ere ari dira nabarmenki euskara maila hobetzen. **Latxa eredua bezain beste?**

Hain zuzen ere hau da nire buruari egiten diodan galdera eredu interesgarri berri bat agertzen den bakoitzean. Eskuz proba batzuk egiteaz gain, ganorazko ebaluazio baten bidez *ranking* bat egitea beharrezkoa zela iruditu zitzaidan. Horrela jaio da [EvalEU](https://itzune.github.io/evaleu/), euskarazko Hizkuntza Ereduen euskara maila neurtu eta alderatzeko proiektua.

Honetarako existitzen diren euskarazko ebaluazio benchmark edo datu-sortak erabili ditut (mila esker *HiTZ* eta *Orai*).

![Hau da momentu honetan dugun rankinga](/images/evaleu_table.png)
![Denboran zehar nola doa aldatzen?](/images/evaleu_timeline.png)

Etorkizunean gehitu nahiko nituzkeen gauzen artean:

- Itzulketa automatikoen ebaluazioak gehitu
- Eredu lokalaz aratago, api bidezko hornitzaileek eskeinitako eredu erraldoiak ere gehitu (OpenAI, Google, Anthropic...)

Proiektua [Itzune](https://itzune.eus) ekimenaren baitan argitaratu dut. Webguneaz gain, [biltegian](https://github.com/itzune/evaleu) ebaluazioak sortzeko erabilitako tresnak ere aurkituko dituzue. Hobekuntzak eta ideiak eskertzen dira!
