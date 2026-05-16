---
title: "Antzoki-TTS: Adding Emotion and Acting Capabilities"
date: 2026-05-16
draft: false
tags: ["ai", "euskara", "tts", "dramabox", "ltx2", "lora", "itzune", "openslr"]
---

Traditional *Text-to-Speech* technology gives us solid voices today, but offers no way to guide the interpretation of the audio. If we want to use these models to produce audiobooks, stories, game audio, etc., we soon realize the results are not ideal. We get cold, neutral voices. Robotic. Boring.

Lately, however, models that allow us to specify paralinguistic cues (pauses, breathing, and emotional variations) are beginning to emerge. Thanks to this technology, by providing script-like instructions, **we can create emotionally rich synthetic voices**.

That is precisely the goal of [Antzoki-TTS](https://huggingface.co/itzune/antzoki-tts), my latest experiment: to be able to define the character's personality, emotional qualities, and these paralinguistic features; and to achieve **clean results in Basque**.

For example, by giving the following instruction (in script format, describing a character and emotions) we can generate a menacing, fearful voice, guided by these references:

> *A shadowy villain speaks with cold menace, "Nire lurretan sartu zara, morroi"
> He chuckles darkly, "Erruz ordainduko duzu."
> His voice rises with fury, "Belaunikatu, edo suntsituko zaitut!!"*

{{< rawhtml >}}
<audio controls preload="metadata">
  <source src="/audio/xabi_test_1.mp3" type="audio/mpeg">
  Your browser does not support the audio tag.
</audio>
{{< /rawhtml >}}

Or, if preferred, a sweeter and more cheerful tone:

> *A bright-eyed girl spins in a field of wildflowers, her voice bubbling with pure, breathless wonder:
> "Aizu, aitona! Entzun duzu?!"
> She laughs, a sound as clear as a mountain stream.
> "Makina batek hitz egiten duela dirudi, baina hain da erreala!"
> She spreads her arms wide, looking up at the sky in disbelief.
> "Sinestezina da... adimen artifizialak nire ahotsa sortu du!!"*

{{< rawhtml >}}
<audio controls preload="metadata">
  <source src="/audio/xabi_test_2.mp3" type="audio/mpeg">
  Your browser does not support the audio tag.
</audio>
{{< /rawhtml >}}

**Antzoki-TTS** is based on the [DramaBox](https://www.resemble.ai/learn/models/dramabox) model, which in turn is built upon the [LTX-2](https://ltx.io/model/ltx-2) video model. Specifically, they extracted the audio generation component from this video model, and the results are remarkable. In my case, I trained a [LoRA](https://huggingface.co/itzune/antzoki-tts) adaptation on top of the original model, with the aim of improving Basque pronunciation and prosody.

## How Does It Work?

In addition to the *director's script* style text prompt, if you also provide an audio file as a reference, the model will use its voice style as a base. Indeed, from what I've seen, this is how the best results are achieved.

The model is fed these two elements:

1. **Reference audio** (~10 seconds is enough, to copy the voice's timbre and style)
2. **Director's script**: which describes not just the text, but also the interpretation — emotions, pauses, breathing...

I recommend writing the scripts in English, but the text inside the quotes is written in Basque, and the results adapt remarkably well.

## Training

For training I used the [OpenSLR76](https://www.openslr.org/76/) dataset, so the model could "learn" Basque. A total of 7,136 recordings from 52 different speakers (29 female, 23 male), amounting to around 14 hours of audio.

Unfortunately, this dataset only contains neutral voices — plain readings — so we could say that the original acting capability has been somewhat diminished. Even so, DramaBox's base model is inherently very expressive, and the results still maintain high quality.

## Usage

To use the model locally, you need to install DramaBox, and then load the LoRA with the `--lora` flag:

```bash
cd DramaBox
CUDA_VISIBLE_DEVICES=0 PYTHONPATH=ltx2 python src/inference.py \
  --checkpoint      dramabox-dit-v1.safetensors \
  --full-checkpoint dramabox-audio-components.safetensors \
  --lora            antzoki-tts/best_step_06850.safetensors \
  --voice-sample    reference.wav \
  --prompt          "Your script..." \
  --output          output.wav
```

For now, approximately 12 GB of VRAM is required. I'm confident that these requirements will decrease over time, until anyone can run it on their ordinary computer.

## Limitations and the Future

The results I've published here are specifically cherry-picked. It does make mistakes from time to time, and I see a lot of room for improvement. Looking ahead, I believe training with expressive data (story narrations, theatrical performances...) would improve it greatly. Technically it doesn't seem particularly difficult, but there are other limitations (intellectual property rights) that would restrict its use.

[The LoRA model is available on Hugging Face](https://huggingface.co/itzune/antzoki-tts), as part of the [Itzune](https://huggingface.co/itzune) project. Feel free to give it a try!
