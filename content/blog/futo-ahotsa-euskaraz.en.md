---
title: "Dictating in Basque on mobile, without sending your voice anywhere"
date: 2026-07-21
description: "A Basque Whisper model for FUTO Keyboard: dictate in Basque on your phone, with everything running on the device and no audio sent anywhere."
images: ["images/futo-ahotsa-euskaraz-en-cover.jpg"]
draft: false
tags: ["ai", "euskara", "basque", "stt", "asr", "whisper", "whisper.cpp", "acft", "futo", "voice-input"]
---

## TL;DR

In my [previous post](/blog/futo-euskaraz) I introduced Basque predictive text for the [**FUTO Keyboard**](https://keyboard.futo.tech/). Now we've added voice typing too: I've prepared [a Basque *Whisper* model](https://huggingface.co/itzune/whisper-small-eu-acft-ggml) for dictating in Basque with FUTO's microphone button. It runs on the phone itself, without sending your voice anywhere.

## Speak instead of typing

When we need to write a long message, it's often easier to just speak. While driving, when our hands are dirty in the kitchen, or simply out of laziness. Voice typing has been on our phones for a long time.

But here, too, the same question: **where does our voice go?** If text is sensitive, voice is even more so. Our voice is ours, and along with it come background sounds, the conversations of people around us... That's a lot of data to send to someone else's server.

FUTO has a solution for this: [*FUTO Voice Input*](https://voiceinput.futo.org/) comes built into the keyboard, and uses [*whisper.cpp*](https://github.com/ggml-org/whisper.cpp) to transcribe directly on the phone. Unfortunately, just as with predictive text, there's no suitable Basque model available.

## Whisper in Basque? We've got that!

Luckily, we don't have to start from scratch. I've been [adapting *Whisper* models to Basque](/blog/whisper-stt-hobekuntza) for a while now, and the `whisper-small-eu` model achieves a 7.63% WER (word error rate) on the *Common Voice* dataset. In terms of size and quality, it strikes a good balance for running on a phone.

It wasn't quite that simple, though. FUTO processes short audio clips in a special way, and regular *Whisper* models get stuck in a loop, repeating words over and over. To fix this, I fine-tuned the model using the [**ACFT**](https://github.com/futo-org/whisper-acft) method published by FUTO itself.

## Results

Some examples, comparing the reference text with what the model transcribed:

| Reference | Transcription | English |
|---|---|---|
| Honek garrantzi handia zuen Ehun Urteko Gerran. | Honek garrantzen biazuen ehun urteko gerran. | This was of great importance in the Hundred Years' War. |
| Osasuna aurkari zuzena da eta, beraz, puntuek balio bikoitza | Osasuna aurkari zuzena da eta beraz, puntuek balio bikoitza dute. | Osasuna is a direct rival and, therefore, the points are worth double. |
| Irungo familia boteretsu bat da Olazabal familia. | Irungo familia boteretsu bat da Olazovan familia. | The Olazabal family is a powerful family from Irun. |

It's not perfect, as you can see. It got a bit confused with the first sentence, and turned the surname *Olazabal* into *Olazovan*. But for everyday use, I think it works really well.

Here it is, dictating in Basque on a phone (turn the sound on!):

{{< rawhtml >}}
<video controls preload="metadata" playsinline style="max-width: 320px; width: 100%; display: block; margin: 0 auto;">
  <source src="/videos/futo-ahotsa-euskaraz.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>
{{< /rawhtml >}}

## How to install it?

1. [Install *FUTO Keyboard*](https://keyboard.futo.tech/#download), if you haven't already (via *Play Store* or *F-Droid*).
2. Make sure Basque is added as a keyboard language (*Settings* > *Languages* > Euskara).
3. Download the [`small_eu_acft_q8_0.bin` model](https://huggingface.co/itzune/whisper-small-eu-acft-ggml/resolve/main/small_eu_acft_q8_0.bin) to your phone (about 264MB).
4. Open the file with the *FUTO Keyboard* app (from your file manager, choosing "Open with").
	- Alternatively: *Settings* > *Languages* > *Import from file*
5. When prompted, associate the model with Basque (*Basque*).

And you're done! Tap the microphone button and speak in Basque.

## Limitations and next steps

- **Size**: 264MB is no small thing. It may run slowly on modest devices. In the future I'd like to prepare lighter versions based on `whisper-base-eu` or `whisper-tiny-eu`.
- **Dialects and informal speech**: the training data is mostly read speech (*Common Voice*, the Basque Parliament...). If we speak the way we do on the street, it will make more mistakes.
- **Evaluation**: so far I've only run a few tests. A more thorough evaluation is still needed.

The models are available [on Hugging Face](https://huggingface.co/itzune/whisper-small-eu-acft-ggml), as part of the [Itzune](https://huggingface.co/itzune) project. Together with predictive text, we now have the full FUTO keyboard in Basque: for typing and for speaking, all on our own phone. Try it out and let me know how it goes!
