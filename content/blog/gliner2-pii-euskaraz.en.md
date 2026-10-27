---
title: "Hiding personal data in Basque texts"
date: 2026-10-10
description: "Adapting GLiNER2 to Basque to detect personal data (names, phone numbers, addresses, IDs...) in texts: an extra layer of protection."
cover:
    image: "/images/gliner2-pii-euskaraz-cover.jpg"
    alt: "A magnifying glass over text"
draft: false
tags: ["ai", "euskara", "basque", "pii", "privacy", "gliner2", "ner", "lora", "tknika"]
---

## What is GLiNER2?

[GLiNER2](https://github.com/fastino-ai/GLiNER2) is a family of models for extracting entities (names, places, dates...) from text. What makes it special is that it has no fixed list of labels: we tell it what we want to find ("person name", "phone number", "email"...), and it looks for those in the text.

Fastino released a version for detecting personal data (*PII*, *Personally Identifiable Information*): [gliner2-privacy-filter-PII-multi](https://huggingface.co/fastino/gliner2-privacy-filter-PII-multi). It has only 205M parameters and doesn't need a GPU.

## And in Basque?

Despite being multilingual, it doesn't work well in Basque. It barely detects addresses, and it often fails with Basque given names and surnames. Our declensions don't help either: in the sentence "Amorebietan bizi naiz" ("I live in Amorebieta"), the whole word *Amorebietan* is the mention of the town, suffix included.

And the opposite problem too: on 159 sentences with no personal data, it produced **225 false positives**.

## How did we improve it?

We mixed two data sources:

- **Basque entities**: [BasqueGLUE](https://huggingface.co/datasets/orai-nlp/basqueGLUE) (Orai), with person, place and organization names from Basque news.
- **Synthetic personal data**: [5,000 made-up sentences](https://huggingface.co/datasets/tknika/pii-synthetic-basque-v2), in Basque, Spanish and French, covering the whole Basque Country. Given names and surnames come from INE and INSEE statistics, streets from OpenStreetMap, and ID, IBAN or card numbers are randomly generated (but valid). No real people's data, of course.

The second one matters, so the model doesn't forget its original abilities while adapting to Basque. We also added new fields that can be useful in education: user names, personal URLs and student IDs.

We trained it with LoRA, in about 6 minutes on a single GPU. Results, on sentence templates never seen during training:

| | F1 | False positives |
|---|---|---|
| Original model | 0.742 | 225 |
| **Adapted to Basque** | **0.905** | **0** |

## And now, what for?

I want to make this clear from the start: this model **is not enough to "clean" data automatically**. It doesn't provide enough guarantees for that. Sensitive data should never be sent to AI providers, and this doesn't replace that practice.

Quite the opposite: it's **one more layer**, to make sure nothing slips through. For example, before sharing a document, to check whether we forgot some piece of personal data:

{{< rawhtml >}}
<video controls preload="metadata" playsinline style="width: 100%; display: block; margin: 0 auto;">
  <source src="/videos/gliner2-pii-euskaraz-demo1.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>
{{< /rawhtml >}}

Or before asking a language model (LLM) for something, to catch a name or phone number we typed without meaning to:

{{< rawhtml >}}
<video controls preload="metadata" playsinline style="width: 100%; display: block; margin: 0 auto;">
  <source src="/videos/gliner2-pii-euskaraz-demo2.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>
{{< /rawhtml >}}

> Keep in mind: the evaluation was done on synthetic data, and results on real texts will be worse. The model is licensed under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) (non-commercial use), because BasqueGLUE has that license.

The model, dataset and code are available on [Hugging Face](https://huggingface.co/tknika/gliner2-PII-basque-v2) and [GitHub](https://github.com/tknika/gliner2-pii-basque).

*Cover image: [Magnifying glass with focus on paper](https://commons.wikimedia.org/wiki/File:Magnifying_glass_with_focus_on_paper.png), Niabot, [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/).*
