---
title: "Euskaraz diktatzen mugikorrean, ahotsa inora bidali gabe"
date: 2026-07-21
description: "FUTO Keyboard-erako euskarazko Whisper eredua: mugikorrean euskaraz diktatzeko, dena telefonoan bertan exekutatuta, ahotsa inora bidali gabe."
cover:
    image: "/images/futo-ahotsa-euskaraz-cover.jpg"
    alt: "Mugikorrari hitz egiten"
draft: false
tags: ["ai", "euskara", "stt", "asr", "whisper", "whisper.cpp", "acft", "futo", "ahots-sarrera"]
---

## TL;DR (Luzeegia; Ez Dut Irakurri)

[Aurreko artikuluan](/blog/futo-euskaraz) [**FUTO Keyboard**](https://keyboard.futo.tech/) teklatuarentzat euskarazko testu prediktiboa aurkeztu nuen. Orain, ahots bidezko idazketa gehitu diogu: [euskarazko *Whisper* eredu bat](https://huggingface.co/itzune/whisper-small-eu-acft-ggml) prestatu dut, FUTOren mikrofono botoiarekin euskaraz diktatzeko. Telefonoan bertan exekutatzen da, ahotsa inora bidali gabe.

## Idatzi beharrean, hitz egin

Mezu luze bat idatzi behar dugunean, askotan errazagoa izaten da hitz egitea. Gidatzen ari garenean, sukaldean eskuak zikin ditugunean, edo besterik gabe alferkeriaz. Ahots bidezko idazketa (ingelesez *voice typing*) aspalditik dago gure mugikorretan.

Baina hemen ere, galdera berbera: **nora doa gure ahotsa?** Testua sentikorra baldin bada, ahotsa are gehiago. Gure ahotsa gurea da, eta ahotsarekin batera, atzeko soinuak, inguruko pertsonen elkarrizketak... Datu asko dira, zerbitzari arrotz batera bidaltzeko.

FUTOk badu horretarako konponbidea: [*FUTO Voice Input*](https://voiceinput.futo.org/) teklatuan bertan integratuta dator, eta [*whisper.cpp*](https://github.com/ggml-org/whisper.cpp) erabiltzen du transkripzioa mugikorrean bertan egiteko. Tamalez, testu prediktiboarekin gertatzen zen bezala, euskarazko eredu egokirik ez dago eskuragarri.

## Whisper euskaraz? Hori badugu!

Zorionez, ez dugu hutsetik hasi beharrik. Aspalditik nabil [*Whisper* ereduak euskarara egokitzen](/blog/whisper-stt-hobekuntza), eta `whisper-small-eu` ereduak %7,63ko WER (hitz-errore tasa) lortzen du *Common Voice* datu-sortan. Tamainaz eta kalitatez, mugikor batean exekutatzeko oreka ona du.

Ez zen hain erraza izan, ordea. FUTOk audio laburrak modu berezian prozesatzen ditu, eta *Whisper* eredu arruntak bukle batean geratzen dira, hitzak behin eta berriz errepikatzen. Hori konpontzeko, FUTOk berak argitaratutako [**ACFT**](https://github.com/futo-org/whisper-acft) metodoa erabiliz doitu dut eredua.

## Emaitzak

Adibide batzuk, erreferentziazko testua eta ereduak transkribatutakoa alderatuz:

| Erreferentzia | Transkripzioa |
|---|---|
| Honek garrantzi handia zuen Ehun Urteko Gerran. | Honek garrantzen biazuen ehun urteko gerran. |
| Osasuna aurkari zuzena da eta, beraz, puntuek balio bikoitza | Osasuna aurkari zuzena da eta beraz, puntuek balio bikoitza dute. |
| Irungo familia boteretsu bat da Olazabal familia. | Irungo familia boteretsu bat da Olazovan familia. |

Ez da perfektua, ikusten denez. Lehenengo esaldiarekin pixka bat nahastu da, eta *Olazabal* abizena *Olazovan* bihurtu du. Baina eguneroko erabilerarako, oso ondo dabilela iruditzen zait.

Hona hemen mugikorrean euskaraz diktatzen (piztu soinua!):

{{< rawhtml >}}
<video controls preload="metadata" playsinline style="max-width: 320px; width: 100%; display: block; margin: 0 auto;">
  <source src="/videos/futo-ahotsa-euskaraz.mp4" type="video/mp4">
  Zure nabigatzaileak ez du bideo etiketa onartzen.
</video>
{{< /rawhtml >}}

## Nola instalatu?

1. [*FUTO Keyboard* instalatu](https://keyboard.futo.tech/#download), oraindik ez baduzu (*Play Store* edo *F-Droid* bidez).
2. Ziurtatu euskara teklatuko hizkuntza gisa gehituta duzula (*Settings* > *Languages* > Euskara).
3. Deskargatu [`small_eu_acft_q8_0.bin` eredua](https://huggingface.co/itzune/whisper-small-eu-acft-ggml/resolve/main/small_eu_acft_q8_0.bin) zure telefonoan (264MB ingurukoa).
4. Ireki fitxategia *FUTO Keyboard* aplikazioarekin (fitxategi kudeatzailetik, "Ireki honekin" aukeratuz).
	- Bestela: *Settings* > *Languages* > *Import from file*
5. Galdetzen dizunean, lotu eredua euskararekin (*Basque*).

Eta prest! Sakatu mikrofonoaren botoia eta hitz egin euskaraz.

## Mugak eta hurrengo urratsak

- **Tamaina**: 264MB ez da gutxi. Gailu xumeetan motel ibil daiteke. Etorkizunean `whisper-base-eu` edo `whisper-tiny-eu` ereduekin bertsio arinagoak prestatu nahiko nituzke.
- **Euskalkiak eta hizketa informala**: entrenamendurako datuak gehienbat testu irakurriak dira (*Common Voice*, Legebiltzarra...). Kalean hitz egiten dugun bezala hitz egiten badugu, akats gehiago egingo ditu.
- **Ebaluazioa**: oraingoz proba gutxi egin ditut. Ebaluazio sakonagoa egitea falta da.

Ereduak [Hugging Face-n](https://huggingface.co/itzune/whisper-small-eu-acft-ggml) eskuragarri daude, [Itzune](https://huggingface.co/itzune) proiektuaren baitan. Testu prediktiboarekin batera, FUTO teklatua osorik dugu euskaraz: idazteko eta hitz egiteko, dena gure mugikorrean. Probatu eta esan zer moduz!

*Partekatzeko irudia: [Woman speaking on phone](https://commons.wikimedia.org/wiki/File:Woman_speaking_on_phone.jpg), Queen Asali, [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).*
