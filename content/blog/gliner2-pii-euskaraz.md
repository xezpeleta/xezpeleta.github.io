---
title: "Datu pertsonalak ezkutatzen euskarazko testuetan"
date: 2026-10-10
description: "GLiNER2 eredua euskarara egokitzen, testuetako datu pertsonalak (izenak, telefonoak, helbideak, NANak...) detektatzeko: babes-geruza gehigarri bat."
draft: false
tags: ["ai", "euskara", "pii", "pribatutasuna", "gliner2", "ner", "lora", "tknika"]
---

## GLiNER2 zer da?

[GLiNER2](https://github.com/fastino-ai/GLiNER2) testu batetik entitateak (izenak, lekuak, datak...) erauzteko eredu familia bat da. Berezitasuna da ez duela aurrez finkatutako etiketa zerrendarik: guk esaten diogu zer bilatu nahi dugun ("pertsona izena", "telefonoa", "posta elektronikoa"...), eta horiek bilatzen ditu testuan.

Fastino-k datu pertsonalak (ingelesez *PII*, *Personally Identifiable Information*) detektatzeko bertsio eleanitza argitaratu zuen duela hilabete gutxi: [gliner2-privacy-filter-PII-multi](https://huggingface.co/fastino/gliner2-privacy-filter-PII-multi). 205M parametro besterik ez ditu, eta ez du GPUrik behar exekutatzeko.

## Eta euskaraz?

Eleaniztuna izan arren, euskaraz ez dabil fin. Euskal izenak, abizenak, helbideak ez ditu ondo detektatzen. Gure deklinabideak ere ez dio asko laguntzen: "Amorebietan bizi naiz" esaldian, hiriaren izen gisa *Amorebietan* hartzen zuen (*Amorebieta* beharrean).

Eta alderantzizko arazoa ere bai: datu pertsonalik gabeko 159 esalditan, **225 faltsu positibo** ematen zituen.

## Nola hobetu dugu?

Bi datu iturri nahastu ditugu:

- **Euskarazko entitateak**: [BasqueGLUE](https://huggingface.co/datasets/orai-nlp/basqueGLUE) (Orai), euskarazko albisteetako pertsona, leku eta erakunde izenekin.
- **Datu pertsonal sintetikoak**: [5.000 esaldi asmatu](https://huggingface.co/datasets/tknika/pii-synthetic-basque-v2), euskaraz, gaztelaniaz eta frantsesez, Euskal Herri osokoak. Izen eta abizenak INE eta INSEEko estatistiketatik, kaleak OpenStreetMap-etik, eta NAN, IBAN edo txartel zenbakiak ausaz sortuak (baina baliozkoak). Inongo pertsona errealen daturik gabe noski.

Bigarren hau garrantzitsua da, eredua euskarara egokitzean jatorrizko gaitasunak ahaztu ez ditzan. Gainera, hezkuntza esparruan baliagarriak izan daitezkeen eremu berriak gehitu ditugu: erabiltzaile izenak, URL pertsonalak eta ikasle zenbakiak.

Entrenamendua LoRA bidez egin dugu, 6 minutu inguru GPU batean. Emaitzak, entrenamenduan inoiz ikusi gabeko esaldi ereduekin:

| | F1 | Faltsu positiboak |
|---|---|---|
| Jatorrizko eredua | 0,742 | 225 |
| **Euskarara egokitua** | **0,905** | **0** |

## Eta orain, zertarako?

Argi utzi nahi nuke hasieratik: eredu hau **ez da nahikoa datuak modu automatikoan "garbitzeko"**. Ez du horretarako berme nahikorik ematen. Datu sentikorrak ez dira inoiz adimen artifizialeko hornitzaileetara bidali behar, eta honek ez du praktika hori ordezten.

Justu kontrakoa: **geruza bat gehiago** da, ezerk ihes egiten ez digula ziurtatzeko. Adibidez, dokumentu bat partekatu aurretik, ahaztu zaigun datu pertsonalen bat dagoen begiratzeko:

{{< rawhtml >}}
<video controls preload="metadata" playsinline style="width: 100%; display: block; margin: 0 auto;">
  <source src="/videos/gliner2-pii-euskaraz-demo1.mp4" type="video/mp4">
  Zure nabigatzaileak ez du bideo etiketa onartzen.
</video>
{{< /rawhtml >}}

Edo hizkuntza eredu bati (LLM) zerbait eskatu aurretik, nahi gabe idatzi dugun izen edo telefono zenbakiren bat harrapatzeko:

{{< rawhtml >}}
<video controls preload="metadata" playsinline style="width: 100%; display: block; margin: 0 auto;">
  <source src="/videos/gliner2-pii-euskaraz-demo2.mp4" type="video/mp4">
  Zure nabigatzaileak ez du bideo etiketa onartzen.
</video>
{{< /rawhtml >}}

> Kontuan izan: ebaluazioa datu sintetikoekin egin da, eta benetako testuetan emaitzak okerragoak izango dira. Ereduak [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) lizentzia du (erabilera ez-komertziala), BasqueGLUE-k lizentzia hori duelako.

Eredua, datu-sorta eta kodea eskuragarri daude: [Hugging Face](https://huggingface.co/tknika/gliner2-PII-basque-v2) eta [GitHub](https://github.com/tknika/gliner2-pii-basque).
