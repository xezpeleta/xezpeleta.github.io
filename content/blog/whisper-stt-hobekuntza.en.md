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

Speech-to-text (STT) technology converts spoken language into written text using natural language processing. These systems are becoming increasingly important in digital interfaces, accessibility solutions, and various communication platforms.

Since 2022, I've been fine-tuning the original [Whisper](https://openai.com/index/whisper/) speech recognition model for the Basque language, using the [Mozilla Common Voice](https://commonvoice.mozilla.org/) dataset. Compared to the original models, I've seen significant improvements in performance. As the Mozilla Common Voice initiative has grown, the model's accuracy has continued to improve.

> However, it became clear that more voice data was needed to achieve an acceptable quality level.

A few weeks ago, I discovered [a new study from the HiTZ-Aholab research center](https://www.isca-archive.org/iberspeech_2024/herranz24_iberspeech.pdf), where they created a bilingual *Nvidia NeMo* model using multiple datasets: Mozilla Common Voice, OpenSLR, and the Basque Parliament corpus.

Inspired by this work, I decided to use the same data collection to improve the Whisper model. The results have improved significantly; for example, the **Word Error Rate (WER) of the `whisper-small-eu` model has decreased from 11.84% to 7.63%**.

## Datasets

Based on the HiTZ-Aholab report, I used the following data collections:

- Mozilla Common Voice
- OpenSLR
- Basque Parliament corpus

The combination of these datasets provides greater diversity in terms of speakers, recording quality, and content domains.

Additionally, researcher Asier Herranz has made these datasets readily accessible: [asierhv/composite_corpus_eu_v2.1](https://huggingface.co/datasets/asierhv/composite_corpus_eu_v2.1). In total, **675.98 hours of training data** are available.

## Results

Results of the new models:
- `whisper-large-v3-eu` model updated, **WER: 4.84%** (previously: 7.21%).
- `whisper-medium-eu` model updated, **WER: 7.14%** (previously: 8.80%)
- `whisper-small-eu` model updated, **WER: 7.63%** (previously: 11.83%)
- `whisper-base-eu` model (new), **WER: 10.78%**
- `whisper-tiny-eu` model (new), **WER: 13.56%**

*Note: Lower WER values indicate better performance.*

The Basque **Whisper** models created are [available here](https://huggingface.co/collections/xezpeleta/whisper-basque-fine-tuning-67b05797b023991df1715a51).

These evaluations were performed using the `test` portion of the `Mozilla Common Voice 18.0` dataset.

## Similar Alternatives

- In addition to the research mentioned earlier, [this work published by Vicomtech](https://www.isca-archive.org/iberspeech_2024/vasquezcorrea24_iberspeech.pdf) is also noteworthy. Using the same dataset, they trained a Basque-Spanish *Whisper* model and achieved **excellent results**. Unfortunately, these models **have not been made publicly available** (as far as I know).
- [HiTZ/stt_eu_conformer_transducer_large](https://huggingface.co/HiTZ/stt_eu_conformer_transducer_large): A Basque Speech-to-Text model based on the Conformer-Transducer architecture. It uses Nvidia NeMo technology and achieves **very impressive results**: 2.79% WER.
- [Elhuyar Aditu](https://aditu.eus/) is also a speech recognition system that performs automatic transcriptions. It is not open source and requires a subscription, but they offer a trial option on their website.