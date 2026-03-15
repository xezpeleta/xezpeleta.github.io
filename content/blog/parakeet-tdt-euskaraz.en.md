---
title: "Nvidia Parakeet in Basque: fast and CPU-friendly"
date: 2026-03-15
draft: false
tags: ["ai", "basque", "stt", "nvidia", "parakeet", "onnx"]
cover:
    image: "/images/parakeet-tdt-euskaraz-cover.png"
    alt: "Nvidia Parakeet in Basque"
    caption: "Parakeet in Basque: fast and CPU-ready"
---

Over the last few days, I have been fine-tuning [Nvidia Parakeet](https://huggingface.co/nvidia/parakeet-tdt-0.6b-v3) for Basque, and I have published the result [here](https://huggingface.co/itzune/parakeet-tdt-0.6b-v3-basque).

The goal was simple: to have a lightweight Basque speech-to-text model that runs fast and is practical on modest hardware.

## Accuracy vs speed

To be clear, this model is not as accurate as my best Basque Whisper model:

- [xezpeleta/whisper-large-v3-eu](https://huggingface.co/xezpeleta/whisper-large-v3-eu)

However, it has a major advantage: it is very fast and can run on CPU-only setups.

> If maximum accuracy is your priority, basque Whisper Large v3 is still the better option. If you prioritize speed and low-resource inference, Parakeet is a strong alternative.

## Recommended format: ONNX

For practical usage, I recommend running this model in ONNX format.

Pre-converted ONNX files are available here:

- [xezpeleta/parakeet-tdt-0.6b-v3-basque-sherpa-onnx](https://huggingface.co/xezpeleta/parakeet-tdt-0.6b-v3-basque-sherpa-onnx)

This makes integration easier and gives good performance, especially in CPU environments.

## About the fine-tuning process

More details about training, metrics, and tracking are available here:

- [W&B report](https://api.wandb.ai/links/xezpeleta/6d1xtga2)

## Short conclusion

For Basque STT right now:

- If you prioritize accuracy: `whisper-large-v3-eu`
- If you prioritize speed and CPU usage: `parakeet-tdt-0.6b-v3-basque` (via ONNX)

