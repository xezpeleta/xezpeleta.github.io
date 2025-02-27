---
title: "Basque from speech to text: improving transcription models"
date: 2024-03-20
draft: false
tags: ["ai", "basque", "stt", "whisper"]
cover:
    image: "/images/stt.png"
    alt: "Speech-to-text"
    caption: "Basque from speech to text"
---

Since 2022, I've been training the original [Whisper](https://openai.com/index/whisper/) STT (*speech-to-text*) model using the [Mozilla Common Voice](https://commonvoice.mozilla.org/) dataset to improve its performance with the Basque language (through [*fine-tuning*](https://en.wikipedia.org/wiki/Fine-tuning_(deep_learning))). *STT* models convert speech to text using natural language processing.

Compared to the original models, there was a significant improvement in results. As the Mozilla Common Voice initiative grew, the model performed much better.

> But at the same time, it became clear that more voice data was needed to achieve a minimum quality level.

A few weeks ago, I found [a new study from the HiTZ-Aholab research center](https://www.isca-archive.org/iberspeech_2024/herranz24_iberspeech.pdf), where they created a bilingual *Nvidia NeMo* model using various datasets: Mozilla Common Voice, OpenSLR, and the Basque Parliament corpus.

Inspired by this work, I decided to use the same data collection to improve the Whisper model. The results have improved significantly; for example, the **WER (Word Error Rate) of the `whisper-small-eu` model has decreased from 11.84% to 7.63%**.

## Datasets

Based on the HiTZ-Aholab report, I used the following data collections:

- Mozilla Common Voice
- OpenSLR
- Basque Parliament

The combination of these datasets provides greater diversity, both in terms of speakers, recording quality, and context and topics.

Additionally, researcher Asier Herranz has made these data ready to use in an easy way: [asierhv/composite_corpus_eu_v2.1](https://huggingface.co/datasets/asierhv/composite_corpus_eu_v2.1). In total, we have **675.98 hours of training data** available.

## Results

Results of the new models:
- `whisper-large-v3-eu` model updated, **WER: 4.84** (previously: 7.21).
- `whisper-medium-eu` model updated, **WER: 7.14** (previously: 8.80)
- `whisper-small-eu` model updated, **WER: 7.63** (previously: 11.83)
- `whisper-base-eu` model (new), **WER: 10.78**
- `whisper-tiny-eu` model (new), **WER: 13.56**

*Note: The lower the WER value, the better.*

The Basque **Whisper** models created are [available here](https://huggingface.co/collections/xezpeleta/whisper-basque-fine-tuning-67b05797b023991df1715a51)

These evaluations were performed using the `test` portion of the `Mozilla Common Voice 18.0` dataset.

## Similar Alternatives

- In addition to the research mentioned earlier, [this other work published by Vicomtech](https://www.isca-archive.org/iberspeech_2024/vasquezcorrea24_iberspeech.pdf) is also interesting. Similarly, and using the same dataset, they trained a Basque-Spanish *Whisper* model and achieved **excellent results**. Unfortunately, these models **have not been made available** (as far as I know).
- [HiTZ/stt_eu_conformer_transducer_large](https://huggingface.co/HiTZ/stt_eu_conformer_transducer_large) Basque Speech-to-Text model Conformer-Transducer. Based on the Nvidia NeMo model and with **very good results**: 2.79% WER.
- [Elhuyar Aditu](https://aditu.eus/) is also a *speech recognizer* that performs automatic transcriptions. It is not free software and is paid, but they offer the option to try it from their website.