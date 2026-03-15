---
title: "Nvidia Parakeet euskaraz: azkarra eta CPUrako egokia"
date: 2026-03-15
draft: false
tags: ["ai", "euskara", "stt", "nvidia", "parakeet", "onnx"]
cover:
    image: "/images/parakeet-tdt-euskaraz-cover.png"
    alt: "Nvidia Parakeet euskaraz"
    caption: "Parakeet euskaraz: azkarra eta CPUrako prest"
---

Azken egunotan [Nvidia Parakeet](https://huggingface.co/nvidia/parakeet-tdt-0.6b-v3) eredua euskarara doitzen aritu naiz, eta emaitza [hemen argitaratu dut](https://huggingface.co/itzune/parakeet-tdt-0.6b-v3-basque).

Helburua argia zen: euskarazko hizketa-ezagutza eredu arin bat edukitzea, exekuzio azkarrarekin eta hardware xumeagoan ere erabilgarria izateko.

## Zehaztasuna eta abiadura

Argi esanda, eredu hau ez da nire euskarazko Whisper bertsio onena bezain zehatza:

- [xezpeleta/whisper-large-v3-eu](https://huggingface.co/xezpeleta/whisper-large-v3-eu)

Hala ere, badu abantaila handi bat: oso azkarra da, eta CPU hutsean exekutatu daiteke.

> Zehaztasun maximoa behar bada, euskarazko Whisper Large v3 da aukera hobea; abiadura eta baliabide gutxiko exekuzioa lehenesten badira, Parakeet aukera oso interesgarria da.

## ONNX formatuan erabiltzea gomendatua

Parakeet euskaraz modu praktikoan erabiltzeko, ONNX formatua gomendatzen dut.

Horretarako, jada bihurtutako fitxategiak hemen daude:

- [xezpeleta/parakeet-tdt-0.6b-v3-basque-sherpa-onnx](https://huggingface.co/xezpeleta/parakeet-tdt-0.6b-v3-basque-sherpa-onnx)

Horrela, integrazioa errazagoa da eta CPU inguruneetan ere errendimendu ona lor daiteke.

## Fine-tuning prozesuari buruz

Entrenamenduari buruzko xehetasun gehiago, metrikak eta jarraipen grafikoak hemen:

- [W&B txostena](https://api.wandb.ai/links/xezpeleta/6d1xtga2)

## Ondorio laburra

Gaur-gaurkoz, euskarazko STT erabilerarako:

- Zehaztasuna lehenetsi nahi baduzu: `whisper-large-v3-eu`
- Abiadura eta CPU erabilera lehenetsi nahi badituzu: `parakeet-tdt-0.6b-v3-basque` (ONNX bidez)
