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

Hizketa-ezagutzaile (STT, *speech-to-text*) motako ereduek ahots-grabazioak testu idatzi bihurtzeko aukera ematen dute, hizkuntza naturalaren prozesamendu automatikoan oinarrituta. Teknologia honek gero eta garrantzi handiagoa hartzen ari da interfaze digitaletan.

2022\. urteaz geroztik, [Mozilla Common Voice](https://commonvoice.mozilla.org/) datu-bilduma erabiliz, jatorrizko [Whisper](https://openai.com/index/whisper/) STT eredua euskararako doitzen aritu naiz, doitze fin teknika (ingelesez *fine-tuning*) bidez. Jatorrizko ereduekin alderatuta, emaitzetan hobekuntza nabarmenak ikusi ditut. Gainera, Mozilla Common Voice ekimena hazten joan den heinean, ereduaren kalitatea are gehiago hobetu da.

> Hala ere, argi geratu da kalitate-maila onargarri bat lortzeko ahots-datu gehiagoren premia dagoela.

Duela aste batzuk, [HiTZ-Aholab ikerketa zentroak egindako lan berri bat](https://www.isca-archive.org/iberspeech_2024/herranz24_iberspeech.pdf) aurkitu nuen. Bertan, *Nvidia NeMo* eredu elebidun bat sortu dute hainbat datu-bilduma ezberdin baliatuz: Mozilla Common Voice, OpenSLR eta Eusko Legebiltzarreko korpusa.

Lan horrek bultzatuta, datu-bilduma bera erabiltzea erabaki dut Whisper eredua hobetzeko. Emaitzak nabarmen hobetu dira; adibidez, `whisper-small-eu` ereduaren **hitz-errore tasa (WER, Word Error Rate) %11,84tik %7,63ra jaitsi da**.

## Datu-bildumak

HiTZ-Aholab txostenean oinarrituta, honako datu-sortak erabili ditut:

- Mozilla Common Voice
- OpenSLR
- Eusko Legebiltzarreko korpusa

Datu-bilduma hauen konbinazioak aniztasun handiagoa eskaintzen du, bai hizlarien aldetik, bai grabazio-kalitatearen aldetik, baita testuinguru eta gai ezberdinen aldetik ere.

Gainera, Asier Herranz ikerlariak datu hauek modu errazean erabiltzeko prestatu ditu: [asierhv/composite_corpus_eu_v2.1](https://huggingface.co/datasets/asierhv/composite_corpus_eu_v2.1). Guztira, **675,98 orduko entrenamendu-datuak** ditugu eskuragarri.

## Emaitzak

Eredu berrien emaitzak:
- `whisper-large-v3-eu` eredua eguneratu da, **WER: %4,84** (lehenago: %7,21).
- `whisper-medium-eu` eredua eguneratu da, **WER: %7,14** (lehenago: %8,80)
- `whisper-small-eu` eredua eguneratu da, **WER: %7,63** (lehenago: %11,83)
- `whisper-base-eu` eredua (berria), **WER: %10,78**
- `whisper-tiny-eu` eredua (berria), **WER: %13,56**

*Oharra: hitz-errore tasa (WER) zenbat eta txikiagoa izan, orduan eta hobea da eredua.*

Sortutako euskarazko **Whisper** ereduak [hemen eskuragarri daude](https://huggingface.co/collections/xezpeleta/whisper-basque-fine-tuning-67b05797b023991df1715a51).

Ebaluazio hauek `Mozilla Common Voice 18.0` datu-sortaren `test` zatia erabiliz egin dira.

## Antzeko alternatibak

- Lehen aipatutako ikerketaz gain, [Vicomtech-ek argitaratutako](https://www.isca-archive.org/iberspeech_2024/vasquezcorrea24_iberspeech.pdf) beste lan hau ere azpimarragarria da. Ildo beretik, eta datu-sorta bera erabiliz, euskara-gaztelaniazko *Whisper* eredua trebatu dute eta **emaitza bikainak** lortu dituzte. Zoritxarrez, eredu hauek **ez dituzte publikoki eskuragarri jarri** (nik dakidala).
- [HiTZ/stt_eu_conformer_transducer_large](https://huggingface.co/HiTZ/stt_eu_conformer_transducer_large): Euskararako hizketa-testu bihurtze eredua, Conformer-Transducer arkitekturan oinarritua. Nvidia NeMo teknologia erabiltzen du eta **oso emaitza onak** lortzen ditu: %2,79ko WER.
- [Elhuyar Aditu](https://aditu.eus/) ere transkripzio automatikoak egiten dituen hizketa-ezagutzaile bat da. Ez da software librea eta ordainpekoa da, baina haien webgunetik probatzeko aukera eskaintzen dute.