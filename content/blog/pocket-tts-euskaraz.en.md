---
title: "Pocket TTS in Basque: real-time speech synthesis on a plain CPU"
date: 2026-10-18
draft: false
tags: ["ai", "euskara", "basque", "tts", "pocket-tts", "kyutai", "omnivoice", "pipertts", "itzune", "bssd"]
---

## TL;DR

I've adapted [Kyutai](https://kyutai.org/)'s [Pocket TTS](https://github.com/kyutai-labs/pocket-tts) model to Basque: [**Pocket TTS Basque**](https://itzune.eus/pocket-tts-basque/). It runs on an ordinary computer's CPU, 3.5 times faster than real time, and it can clone voices.

## Filling a gap

Interesting options for Basque speech synthesis have appeared in recent months. [I wrote earlier](/blog/euskarazko-ahots-sintesirako-ereduak) about the Piper TTS and OmniVoice models. But they sit at two extremes:

- **Piper TTS**: light and fast, it runs on any device. But its quality is limited, and it can't clone voices.
- **OmniVoice**: excellent quality and voice cloning. But it's much bigger and heavier.

Pocket TTS sits between the two. It has around 100M parameters (much smaller than OmniVoice), runs in real time on a plain CPU, offers higher quality than Piper and can also clone voices: a clean 5-10 second recording is enough.

## The usual problem: data

We have quite a lot of Basque data for ASR (speech recognition): Common Voice, OpenSLR, the Basque Parliament... But when it comes to training TTS models, we're always struggling. You need high-quality recordings, made in silence, from the same speaker, with the right permissions. And there are few of those.

That's why **I created a synthetic dataset**: [BSSD](https://huggingface.co/datasets/itzune/bssd) (*Basque Synthetic Speech Dataset*). 470 hours of Basque audio, generated with OmniVoice, using voices with the right permissions:

- **Maider and Antton**: the two professional speakers from [HiTZ-Aholab](https://zenodo.org/records/17952596) (CC BY 4.0).
- **The 52 volunteers of [OpenSLR 76](https://www.openslr.org/76/)** (CC BY-SA 4.0), who recorded specifically for TTS.

To generate that audio, I took texts from Wikipedia, Common Voice, openly licensed news and Wikisource. Every generated clip was transcribed with two ASR models, and only the error-free ones were kept.

## How did I train it?

First, I adapted Kyutai's large 24-layer model to Basque. Then I "distilled" it into a smaller 6-layer model: the large model acted as a teacher, and the small one learned to imitate its pronunciation and prosody. That way it keeps the quality while being much faster.

## Listen

Maider, with Pocket TTS Basque:

{{< rawhtml >}}
<audio controls preload="metadata">
  <source src="/audio/pocket-tts-maider.mp3" type="audio/mpeg">
  Your browser does not support the audio tag.
</audio>
{{< /rawhtml >}}

The same sentence, with Piper TTS:

{{< rawhtml >}}
<audio controls preload="metadata">
  <source src="/audio/pocket-tts-piper-maider.mp3" type="audio/mpeg">
  Your browser does not support the audio tag.
</audio>
{{< /rawhtml >}}

And with OmniVoice:

{{< rawhtml >}}
<audio controls preload="metadata">
  <source src="/audio/pocket-tts-omnivoice-maider.mp3" type="audio/mpeg">
  Your browser does not support the audio tag.
</audio>
{{< /rawhtml >}}

Antton:

{{< rawhtml >}}
<audio controls preload="metadata">
  <source src="/audio/pocket-tts-antton.mp3" type="audio/mpeg">
  Your browser does not support the audio tag.
</audio>
{{< /rawhtml >}}

You'll find more examples (five voices, and a comparison of the three models) on the [project's website](https://itzune.eus/pocket-tts-basque/). They aren't cherry-picked: all of them were generated on a CPU, with no manual selection.

## How to use it?

If you have [`uv`](https://docs.astral.sh/uv/) installed, a single command is enough:

```bash
uvx pocket-tts generate --config hf://itzune/pocket-tts-basque/basque.yaml \
  --voice hf://itzune/pocket-tts-basque/voices/Maider.safetensors \
  --text "Kaixo! Hau euskarazko ahots sintetiko bat da." --output kaixo.wav
```

If you want to use your own voice, pass your recording to the `--voice` option (`--voice my_voice.wav`).

> The text must be written the way it should be read: numbers, dates and abbreviations spelled out in words.

## Limitations

It's not perfect. Some words aren't pronounced correctly, for example **"Antton"** or **"onddo"**.

The model, dataset and code are available on [Hugging Face](https://huggingface.co/itzune/pocket-tts-basque) and [GitHub](https://github.com/itzune/pocket-tts-basque), as part of the [Itzune](https://itzune.eus) project. Try it out and let me know how it goes!
