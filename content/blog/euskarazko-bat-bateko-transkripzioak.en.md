---
title: "Real-time Transcriptions in Basque"
date: 2024-03-04
draft: false
tags: ["ai", "euskara", "stt", "whisper"]
cover:
    image: "/images/basque-transcription-animation.svg"
    alt: "Real-time transcription"
    caption: "Animation depicting real-time transcription (Claude 3.7)"
---

In international conferences and events, it is increasingly common to have automatic real-time transcriptions available during live presentations.

![London Bett talk with live transcriptions](/images/london_bett.jpg)

These technologies are very valuable as accessibility measures. Not only for people with hearing problems or cognitive difficulties but [also for those who do not fully master the language](https://eos.org/opinions/caption-this-best-practices-for-live-captioning-presentations).

## Is something like this possible in Basque?

So far, the examples I've seen are in English. Taking advantage of the fact that I recently [published new Whisper models for Basque]({{< ref "whisper-stt-hobekuntza" >}}), I decided to conduct a small experiment. Using a small and lightweight model like `whisper-tiny-eu`, would we be able to create automatic real-time transcriptions in Basque?

## *Whisper-streaming* as the foundation

I took the [Whisper-streaming](https://github.com/ufal/whisper_streaming) project as a base and added the option to publish transcriptions through a web interface. This way, this web page can be used as an overlay in video recording or streaming applications like [OBS](https://obsproject.com).

The results can be seen in the following video:

{{< youtube 5Ix7Xs7AyqA >}}

## What's next?

The *whisper-streaming* project I used runs on [faster-whisper](https://github.com/SYSTRAN/faster-whisper) under the hood. On the other hand, with [whisper.cpp](https://github.com/ggerganov/whisper.cpp), which I really like, there is also an [option](https://github.com/ggerganov/whisper.cpp?tab=readme-ov-file#real-time-audio-input-example) to create real-time transcriptions. I would like to compare both to see which one is faster.

Unfortunately, I don't think I'll have much time for this...

## ENUŔI

For now, to not forget these tests, besides writing this article, I've made the code used available in a project called [ENUŔI](https://github.com/xezpeleta/enuri). If you want to experiment with tools like this, get in touch!