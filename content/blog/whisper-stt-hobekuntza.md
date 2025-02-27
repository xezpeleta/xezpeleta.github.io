---
title: "Euskara hortzetik hitzera: transkripzio ereduak hobetzen"
date: 2024-03-20
draft: false
tags: ["ai", "euskara", "stt", "whisper"]
cover:
    image: "/images/stt.png"
    alt: "Speech-to-text"
    caption: "Euskara hortzetik hitzera"
---

2022tik hasita, [Mozilla Common Voice](https://commonvoice.mozilla.org/) datu sorta erabiliz, jatorrizko [Whisper](https://openai.com/index/whisper/) STT (*speech-to-text*) eredua trebatzen joan naiz euskaraz hobeto egiteko ([*fine-tuning*](https://en.wikipedia.org/wiki/Fine-tuning_(deep_learning)) bat eginez). *STT* ereduek ahotsa testu bihurtzen dute, hizkuntza naturalaren prozesamendu automatikoan oinarrituta.

Jatorrizko ereduekin alderatuta, emaitza asko hobetzen zela ikusten zen. Eta, Mozilla Common Voice ekimena handitu hala, eredua askoz hobeto zebilen.

> Baina aldi berean, kalitate maila minimo bat izateko, ahots datu gehiagoren beharra ere garbi geratzen zen.

Duela aste batzuk, [HiTZ-Aholab ikerketa zentroko lan berri bat](https://www.isca-archive.org/iberspeech_2024/herranz24_iberspeech.pdf) aurkitu nuen, non *Nvidia NeMo* eredu elebidun bat sortu duten hainbat datu sorta ezberdin erabiliz: Mozilla Common Voice, OpenSLR eta Eusko Legebiltzarreko korpusa.

Lan honek inspiratuta, datu bilduma bera erabiltzea erabaki dut Whisper eredua hobetzeko. Emaitzak nabarmen hobetu dira; adibide modura, `whisper-small-eu` ereduaren **WER (Word Error Rate) errorea %11.84tik %7.63ra jaitsi da**.

## Datu sortak

HiTZ-Aholab txosten horretan oinarrituta, honako datu bilduma hauek erabili ditut:

- Mozilla Common Voice
- OpenSLR
- Basque Parliament

Dataset hauen konbinazioak aniztasun handiagoa eskaintzen du, bai hizlarien aldetik, bai grabazio kalitatearen aldetik, eta baita testuinguru eta gai desberdinen aldetik ere.

Gainera, gauzak errezteko, datu hauek modu errezean erabiltzeko prest utzi ditu Asier Herranz ikerlariak: [asierhv/composite_corpus_eu_v2.1](https://huggingface.co/datasets/asierhv/composite_corpus_eu_v2.1). Guztira, **entrenamendu datu kopurua: 675.98 ordu** ditugu eskuragarri.

## Emaitzak

Eredu berrien emaitzak:
- `whisper-large-v3-eu` eredua eguneratu da, **WER: 4.84** (lehenago: 7.21).
- `whisper-medium-eu` eredua eguneratu da, **WER: 7.14** (lehenago: 8.80)
- `whisper-small-eu` eredua eguneratu da, **WER: 7.63** (lehenago: 11.83)
- `whisper-base-eu` eredua (berria), **WER: 10.78**
- `whisper-tiny-eu` eredua (berria), **WER: 13.56**

*Oharra: geroz eta WER balio txikiagoa, hobea.*

Sortutako euskarazko **Whisper** ereduak [eskuragarri dituzue hemen](https://huggingface.co/collections/xezpeleta/whisper-basque-fine-tuning-67b05797b023991df1715a51)

Ebaluazio hauek `Mozilla Common Voice 18.0` dataset-aren `test` zatia erabiliz egin dira.

## Antzeko alternatibak

- Lehen aipatutako ikerketaz gain, [Vicomtech-ek argitaratu duen](https://www.isca-archive.org/iberspeech_2024/vasquezcorrea24_iberspeech.pdf) beste lan hau ere interesgarria da. Ildo beretik, eta datu sorta berdina erabiliz, euskara-gaztelerazko *Whisper* eredua trebatu dute eta **emaitza bikainak** lortu dituzte. Tamalez, eredu hauek **ez dituzte eskuragarri utzi** (nik dakidala).
- [HiTZ/stt_eu_conformer_transducer_large](https://huggingface.co/HiTZ/stt_eu_conformer_transducer_large) Basque Speech-to-Text model Conformer-Transducer. Nvidia NeMo ereduan oinarrituta eta **emaitza oso onak** dituenak: 2.79% WER.
- [Elhuyar Aditu](https://aditu.eus/) ere transkripzio automatikoak egiten dituen *hizketa ezagutzailea* da. Ez da software askea eta ordainpekoa da, bainan haien webgunetik probatzeko aukera eskeintzen dute.