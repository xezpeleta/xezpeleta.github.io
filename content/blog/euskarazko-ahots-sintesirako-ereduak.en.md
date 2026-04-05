---
title: "New Text-to-Speech Models for Basque: Maider, Antton and OmniVoice"
date: 2026-04-04
draft: false
tags: ["ai", "basque", "tts", "hitz", "aholab", "itzune", "pipertts", "omnivoice", "xiaomi"]
---

In recent years, text-to-speech (*TTS*) models have advanced enormously. Month after month, new releases improved pronunciation, prosody, and overall audio quality. Unfortunately, most of those models were designed for English, or at best compatible with only a few languages.

The tools available for generating Basque voices used to be quite limited: paid proprietary systems (such as [Elhuyar's neural TTS, developed by Orai](https://ttsneuronala.elhuyar.eus/)), or older robotic voices that had clearly fallen behind.

Fortunately, this landscape has started to change over the last few months.

## *Maider* and *Antton*, models released by the HiTZ center

[The HiTZ center has released its TTS models](https://huggingface.co/collections/HiTZ/tts). Within the ILENIA project, they published two voices: Antton (male) and Maider (female). These models can be run locally on your own computer or, if preferred, used directly through [Aholab's website](https://aholab.ehu.eus/DNN/TTS/) without installing anything.


{{< rawhtml >}}
<audio controls preload="metadata">
  <source src="/audio/tts_aholab_maider_demo.mp3" type="audio/mpeg">
  Your browser does not support the audio element.
</audio>
{{< /rawhtml >}}


## Basque voices in Piper TTS

Using those two voices released by HiTZ, [Urtzi Odriozola adapted them for Piper TTS](https://blogak.eus/urtzai/maider-eta-antton-euskarazko-tts-ahotsak-piper-motorrerako-egokitu-ditut). [Piper TTS](https://github.com/OHF-Voice/piper1-gpl) is a lightweight and fast text-to-speech engine. Thanks to this, we can generate synthetic voices quickly even on modest devices.

If you want, without installing anything, [I also created a website to synthesize these voices locally](https://itzune.github.io/basque-piper-tts/) using WebAssembly.


{{< rawhtml >}}
<audio controls preload="metadata">
  <source src="/audio/tts_itzunepiper_demo.mp3" type="audio/mpeg">
  Your browser does not support the audio element.
</audio>
{{< /rawhtml >}}

## OmniVoice (Xiaomi)

The best-known TTS models that became popular in recent years ([Coqui](https://github.com/coqui-ai/tts), [Kokoro](https://huggingface.co/hexgrad/Kokoro-82M), [StyleTTS2](https://styletts2.github.io/), [VibeVoice](https://github.com/microsoft/VibeVoice), ...) share several common features:

- **Voice cloning**: in addition to text, you provide a short reference recording and the output is generated in that voice
- **Emotion control**: the ability to generate expressions like laughter, surprise, sighs, etc., via tags

And of course, more "realistic" voices that are increasingly hard to distinguish from real recordings.

Well, surprise: *Xiaomi Corp.* recently published a model that checks all those boxes: [**OmniVoice**, capable of synthesizing more than 600 languages](https://github.com/k2-fsa/OmniVoice).

{{< rawhtml >}}
<audio controls preload="metadata">
  <source src="/audio/omnivoice_demo.mp3" type="audio/mpeg">
  Your browser does not support the audio element.
</audio>
{{< /rawhtml >}}

From the tests I ran, it performs very well in Basque, with high naturalness. It also supports emotion control, for example by adding the *[laughter]* tag to inject laughter. In practice, this emotion control is not yet very reliable in Basque, but still, it feels like an important step forward.

> *"[surprise-wa] hau euskarazko testu batetik sortutako audio bat da!"*

{{< rawhtml >}}
<audio controls preload="metadata">
  <source src="/audio/omnivoice_demo_tag.mp3" type="audio/mpeg">
  Your browser does not support the audio element.
</audio>
{{< /rawhtml >}}

On the other hand, although it can run on a regular computer, inference is relatively heavy and slow. Generating audio for even a short, simple sentence can take around 5 minutes. So in practice, it will likely be more common to run this kind of model on machines or servers with a GPU.

Regarding voice cloning, based on my tests I recommend using a short reference audio clip (<20s), preferably without long silence segments. Generation also takes longer in this mode (more than twice as long).

For now, the [OmniVoice demo site](https://huggingface.co/spaces/k2-fsa/OmniVoice) can be used to run tests.

## Conclusions

When we need instant synthesis, and especially to run locally on almost any device, Basque Piper TTS models are now a practical option. It can be a great companion to the [Basque Parakeet](/blog/parakeet-tdt-euskaraz) speech recognition model.

On the other hand, when we need high-quality Basque voice generation with greater control over the output, **OmniVoice** looks like a very interesting option. That said, for this use case you will likely need a computer or server with a GPU.
