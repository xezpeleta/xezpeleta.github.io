---
title: "Pocket TTS euskaraz: ahots sintesia denbora errealean, CPU soil batean"
date: 2026-10-18
cover:
    image: "/images/pocket-tts-euskaraz-cover.jpg"
    alt: "Mikrofono urdina"
description: "Pocket TTS euskarara egokituta: CPU soil batean denbora errealean dabilen ahots sintesia, ahotsak klonatzeko aukerarekin eta 470 orduko datu-sorta sintetiko batekin."
draft: false
tags: ["ai", "euskara", "tts", "pocket-tts", "kyutai", "omnivoice", "pipertts", "itzune", "bssd"]
---

## TL;DR (Luzeegia; Ez Dut Irakurri)

[Kyutai](https://kyutai.org/)-ren [Pocket TTS](https://github.com/kyutai-labs/pocket-tts) eredua euskarara egokitu dut: [**Pocket TTS Basque**](https://itzune.eus/pocket-tts-basque/). Ordenagailu arrunt baten CPUan exekutatzen da, denbora errealean baino 3,5 aldiz azkarrago, eta ahotsak klonatzeko gai da.

## Hutsune bat betetzen

Euskarazko ahots sintesian, azken hilabeteetan aukera interesgarriak agertu dira. [Lehenago idatzi nuen](/blog/euskarazko-ahots-sintesirako-ereduak) Piper TTS eta OmniVoice ereduen inguruan. Baina bi muturretan daude:

- **Piper TTS**: arina eta azkarra, edozein gailutan dabil. Baina kalitatea mugatua da, eta ezin da ahotsik klonatu.
- **OmniVoice**: kalitate bikaina eta ahotsak klonatzeko aukera. Baina askoz handiagoa eta astunagoa da.

Pocket TTS bien artean dago. 100M parametro inguru ditu (OmniVoice baino askoz txikiagoa), CPU soil batean denbora errealean dabil, Piper baino kalitate handiagoa du eta ahotsak klonatzeko aukera ere badu: 5-10 segundoko grabazio garbi bat nahikoa da.

## Betiko arazoa: datuak

ASRrako (ahots-ezagutzarako) euskarazko datu dexente ditugu: Common Voice, OpenSLR, Legebiltzarra... Baina TTS ereduak entrenatzeko, beti gabiltza larri. Kalitate handiko grabazioak behar dira, isiltasunean, hiztun berberarenak, baimen egokiekin. Eta horrelakoak gutxi dira.

Hau dela eta, **datu-sorta sintetiko bat sortu dut**: [BSSD](https://huggingface.co/datasets/itzune/bssd) (*Basque Synthetic Speech Dataset*). 470 ordu euskarazko audio, OmniVoice bidez sortuak, baimen egokiak dituzten ahotsak erabiliz:

- **Maider eta Antton**: [HiTZ-Aholab](https://zenodo.org/records/17952596)-eko bi hiztun profesionalak (CC BY 4.0).
- **[OpenSLR 76](https://www.openslr.org/76/)-ko 52 boluntarioak** (CC BY-SA 4.0), TTSrako grabatu zutenak.

Audio horiek sortzeko, testuak Wikipedia, Common Voice, lizentzia irekiko albisteak eta Wikisource-tik hartu ditut. Sortutako audio guztiak bi ASR eredurekin transkribatu, eta akatsik gabekoak bakarrik gorde ditut.

## Nola entrenatu dut?

Lehenik, Kyutai-ren 24 geruzako eredu handia euskarara egokitu dut. Ondoren, 6 geruzako eredu txikiago batera "destilatu" dut: eredu handiak irakasle gisa jardun du, eta txikiak haren ahoskera eta prosodia imitatzen ikasi du. Horrela, kalitatea mantenduz, askoz azkarragoa da.

## Entzun

Maider, Pocket TTS Basque bidez:

{{< rawhtml >}}
<audio controls preload="metadata">
  <source src="/audio/pocket-tts-maider.mp3" type="audio/mpeg">
  Zure nabigatzaileak ez du audio etiketa onartzen.
</audio>
{{< /rawhtml >}}

Esaldi bera, Piper TTS bidez:

{{< rawhtml >}}
<audio controls preload="metadata">
  <source src="/audio/pocket-tts-piper-maider.mp3" type="audio/mpeg">
  Zure nabigatzaileak ez du audio etiketa onartzen.
</audio>
{{< /rawhtml >}}

Eta OmniVoice bidez:

{{< rawhtml >}}
<audio controls preload="metadata">
  <source src="/audio/pocket-tts-omnivoice-maider.mp3" type="audio/mpeg">
  Zure nabigatzaileak ez du audio etiketa onartzen.
</audio>
{{< /rawhtml >}}

Antton:

{{< rawhtml >}}
<audio controls preload="metadata">
  <source src="/audio/pocket-tts-antton.mp3" type="audio/mpeg">
  Zure nabigatzaileak ez du audio etiketa onartzen.
</audio>
{{< /rawhtml >}}

Adibide gehiago (bost ahots, eta hiru ereduen arteko alderaketa) [proiektuaren webgunean](https://itzune.eus/pocket-tts-basque/) aurkituko dituzue. Ez daude bereziki aukeratuta: guztiak CPUan sortuak dira, eskuz hautatu gabe.

## Nola erabili?

[`uv`](https://docs.astral.sh/uv/) instalatuta baduzu, komando bakar batekin:

```bash
uvx pocket-tts generate --config hf://itzune/pocket-tts-basque/basque.yaml \
  --voice hf://itzune/pocket-tts-basque/voices/Maider.safetensors \
  --text "Kaixo! Hau euskarazko ahots sintetiko bat da." --output kaixo.wav
```

Zure ahotsa erabili nahi baduzu, `--voice` aukeran zure grabazioa jarri (`--voice nire_ahotsa.wav`).

> Testua irakurri behar den bezala idatzi behar da: zenbakiak, datak eta laburdurak hitzez.

## Mugak

Ez da perfektua. Hitz batzuk ez ditu ondo ahoskatzen, adibidez **"Antton"** edo **"onddo"**.

Eredua, datu-sorta eta kodea eskuragarri daude: [Hugging Face](https://huggingface.co/itzune/pocket-tts-basque) eta [GitHub](https://github.com/itzune/pocket-tts-basque), [Itzune](https://itzune.eus) proiektuaren baitan. Probatu eta esan zer moduz!

*Partekatzeko irudia: [Blue condenser microphone](https://commons.wikimedia.org/wiki/File:Blue_condenser_microphone_(Unsplash).jpg), Kelly Sikkema, [CC0](https://creativecommons.org/publicdomain/zero/1.0/).*
