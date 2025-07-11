---
title: "Zehaztasun handiko azpitituluak"
date: 2024-03-05
draft: true
tags: ["ai", "euskara", "stt", "whisper"]
cover:
    image: "/images/basque-transcription-animation.svg"
    alt: "Transcriptions with high accuracy timestamps"
    caption: "AI generated image"
---

Azkenaldian bideo eduki asko transkribatu behar izan ditut, laneko kontuak direla eta. Konturatu naiz, sortutako azpitituluetan maiz zehastasuna falta zela denbora-marketan. Ez dira akats oso larriak, bainan konbentzituta nengoen egon behar zela moduren bat zehaztasun akats hauek ekiditeko.

Aldi berean, aurretik buruan nuen ideia bat etorri zait burura; *"forced alignment"* delakoa erabiltzea. Hau da, bideoaren audio-edukia eta transkripzioa bera lerrokatzea, hitz bakoitza noiz ahoskatzen den zehaztasunez kalkulatu ahal izateko.

## Indarrezko lerrokatzea

Teknika hau, besteak beste, ahotsezko datu-bildumak sortzeko erabili ohi da. Hainbat tresna existitzen dira lerrokatze automatiko hauek egiteko. Kasu honetan, [WhisperX](https://github.com/m-bain/whisperX) erabili dut.

Adibidez, demagun bideo baten zehaztasun handiko azpitituluak sortu nahi ditugula. Horretarako, honako hauek beharko ditugu:

- Whisper eredua (CTranslate2 formatuan): transkripzioa egiteko
- Lerrokatze eredua (wav2vec2 ereduan oinarritua): hitz mailako zehaztasuna lortzeko. Whisper-ek automatikoki aukeratuko du lerrokatze eredua ezarritasko hizkuntzaren baitan.

```bash
whisperx myaudio.wav --language en --model Systran/faster-whisper-large-v3
```