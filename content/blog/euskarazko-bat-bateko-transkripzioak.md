---
title: "Euskarazko bat-bateko transkripzioak"
date: 2024-03-04
draft: false
tags: ["ai", "euskara", "stt", "whisper"]
cover:
    image: "/images/basque-transcription-animation.svg"
    alt: "Real-time transcription"
    caption: "Zuzeneko trankripzioa irudikatzeko animazioa (Claude 3.7)"
---

Nazioarteko kongresu eta jardunaldietan, geroz eta ohikoagoak dira bat-bateko transkripzio automatikoak eskuragarri izatea zuzeneko hitzaldietan.

![London Bett talk with live transcriptions](/images/london_bett.jpg)

Teknologia hauek irisgarritasun-neurri gisa oso baliagarriak dira. Ez soilik entzumen-arazoak dituzten pertsonentzat edo arazo kognitiboak dituztenentzat, [baita hizkuntza erabat menperatzen ez dutenentzat ere](https://eos.org/opinions/caption-this-best-practices-for-live-captioning-presentations).

## Euskaraz horrelako zeozer posible al da?

Orain arte ikusi ditudan adibideak ingelesez egiten dira. Duela gutxi euskarazko [Whisper eredu berriak argitaratu nituela]{{< ref "whisper-stt-hobekuntza" >}} aprobetxatuz, esperimentu txiki bat egitea erabaki nuen. `whisper-tiny-eu` bezalako eredu txiki eta arin bat erabiliz, gai izango ote zen euskarazko bat-bateko transkripzio automatikoa egiteko?

## *Whisper-streaming* oinarri gisa

[Whisper-streaming](https://github.com/ufal/whisper_streaming) proiektua oinarri gisa hartu eta transkripzioak web interfaze baten bidez argitaratzeko aukera gehitu nion. Horrela, web orri hau *overlay* modura erabil daiteke ondoren [OBS](https://obsproject.com) bezalako bideo grabaketa edo streaming aplikazioetan.

Emaitzak hurrengo bideoan ikus daitezke:

{{< youtube 5Ix7Xs7AyqA >}}

## Eta orain zer?

Erabilitako *whisper-streaming* proiektuak, [faster-whisper](https://github.com/SYSTRAN/faster-whisper) erabiltzen du azpitik. Beste alde batetik, oso gustoko dudan [whisper.cpp](https://github.com/ggerganov/whisper.cpp) alternatibarekin ere [badago aukera](https://github.com/ggerganov/whisper.cpp?tab=readme-ov-file#real-time-audio-input-example) bat-bateko transkripzioak egiteko. Biak alderatu nahiko nituzke, ea zein den azkarragoa.

Tamalez, ez dut uste denbora askorik izango dudanik honetarako...

## ENUŔI

Momentuz, egindako proba hauek ez ahazteko, artikulu hau idazteaz gain, erabilitako kodea [ENUŔI](https://github.com/xezpeleta/enuri) izeneko proiektuan utzi dut eskuragarri. Horrelako tresnekin probak egin nahi badituzu, jarri harremanetan!