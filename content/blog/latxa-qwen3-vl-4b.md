---
title: "Latxa Qwen3 VL 4B eredua"
date: 2026-02-07
draft: false
tags: ["llm", "hitz", "ai", "qwen", "euskarazko ereduak"]
cover:
    image: "/images/latxa-vl-cover.png"
    alt: "Latxa VL eredua"
    caption: "AI generated image"
---

Duela gutxi HiTZ zentroak [Latxa VL](https://huggingface.co/collections/HiTZ/latxa-vl) ereduak argitaratu zituen. Eredu hauek Qwen3-VL ereduetan oinarrituak daude eta ikusmenerako gaitasuna dute.

Momentuz, bi tamaina ditugu eskuragarri, biak oso txikiak: 2B eta 4B parametro dituzten ereduak. Ondorenera aurkeztutako probak 4B ereduarekin eginak izan dira.

## Euskaraz dakiten ereduak

Orokorrean, horrelako tamaina txikiko ereduek ingelesez txukun erantzuteko gaitasuna izan ohi dute soilik. Latxa VL eredu hauek, ordea, euskaraz egiteko entrenatuak izan dira.

![Latxa-VL agurra](/images/latxa-vl-agurra.png)

Euskaraz ulertzeko gai izan harren, sarri akats batzuk egiten ditu erantzunetan.

![Latxa-VL galdera erantzunetan](/images/latxa-vl-galdera.png)

## Irudiak ulertzeko gaitasuna

VL eredu mota hauen berezitasuna ikusmenerako gaitasuna da. Kasu honetan, gainera, eskaera euskaraz egin eta euskaraz erantzuteko gai dela ikus dezakegu.

![Latxa-VL irudia deskribatzen](/images/latxa-vl-porrotx.png)

Aurreko adibidean bezala, irudiak deskribatzeko erabili dezakegu, nahiz eta zehaztasun falta igertzen zaion kasu askotan.

Aldiz, Qwen3-VL ama eredua bezala, Latxa VL bikaina da OCR gisa erabiltzeko. Hau da, irudi batean dagoen testua erauzteko.

![Latxa-VL OCR modura](/images/latxa-vl-ticket.png)

Kasu honetan, ticket baten argazkia eman diot eta bertako informazio guztia eman diezadala eskatu diot.

![Ticket demo](/images/ticket_demo.jpeg)

Hau izan da bere erantzuna:

```
Eskerrik asko zure mezuagatik! Irudiaren informazioa zehatz-mehatz bildu dut, baina garrantzitsua da ohartzea dokumentu honek faktura bat dela, eta ez ordainagiri bat. Hemen duzu irudiko datu guztien zerrenda:

Dokumentuaren Titulua

Autopista Vasco-Aragonesa C.E.S.A.U.
- Anuntzibai auzoa z.g./Barrio Anuntzibai, s/n
- 48410 OROZKO (Bizkaia)
- IFZ/N.I.F.: A-2833764

Ordainagiriaren Datuak
- Ordainagiria: Igarotze Ordainagiria / Comprobante de Paso
- Data eta Ordua: 25/09/23, 00:07

Ordainketa Informazioa
- ID: 08501528326800005
- Ibilbidea / Recorrido: Ibilbidea (ez dago zehaztua)
- Enlace AP-1 AC.: 07 Enlace AP-1 AC.
- Bidearen Informazioa:
    - Bide/Área: 50
    - Bilbao Bideko sarrera/IRTEERA/SALIDA: 15

Ordainketa Modua
- Kontaktu gabeko ordainketa: ARC 00
- Banku Identifikazioa (AID): A000000031010
- Ordainagiriaren aplikazioa (APP): VISA CONTACTLESS
- Autonomia Erregionala (AUT): 065821
- VISA Txartelaren Zenbakia: 476663XXXXX2151

Ordainketa Informazioa
- Zenbatekoa/Importe: 11,30 EUR
- BEZa: %21,00ko BEZ barne
- Kontaktu gabeko ordainketa: CONTACTLESS
- BEZaren barnean sartuta: Incluido. IVA 21,00%
- Deskonturik ez: Agiri honek ez du deskonturik aplikatzen / Este documento no contempla descuentos aplicables

Kontaktu Informazioa
- Bidai Ona / Buen Viaje: F.U.C. 059020891

Dokumentu honen xedea da erabiltzaileak autopistako ordainketa egiaztatzea eta faktura bezala funtzionatzen du, ez ordainagiri gisa. Hala ere, irudiko datu guztiak biltzeko ahalegina egin dut. Zalantzarik izanez gero, jarri harremanetan!
```

Ikus bezala, bertako informazio gehiena ateratzeko gai da, ia akatsik gabe. Esango nuke, gainera, euskarazko testuak hobeto erauzteko gaitasuna duela, Qwen3-VL ereduekin alderatuz. Nahiz eta hau ziurtatzeko, ebaluazio zehatzagoa beharko genukeen.

## Irteera egituratua

Azken urtean argitaratutako eredu berri hauek duten beste berezitasun interesgarri bat, irteera egituratua lortzeko gaitasuna da. Hau da, CSV taula edo JSON egitura duten irteerak lortu ditzakegu gure eskaerei modu zehatz batean erantzuteko.

Honi esker, eredu hauek automatizazio lan fluxuetan integratu ditzakegu. Adibidez, ticketen irudiak pasa eta bertatik informazio zehatza beti modu berean lortu nahiko bagenu, ondorengo n8n automatziazio hau erabili genezake.

![latxa-vl eredua n8n automatizazio batean](/images/latxa-vl-n8n.png)

![latxa-vl ereduari esker irteera egituratua](/images/latxa-vl-n8n-2.png)


## Tresnen erabilera

Irteera egituratuak tresnen erabilera errazten du. Horrela, MCP zerbitzari bat konfiguratu dezakegu gure AA agentean eta bertako tresnak ereduari eskuragarri utzi behar dituenean erabili ditzan.

Tresna hauei deiak ondo egiten dizkiela konprobatu dut baina, tamalez, egin dudan probetan tresnaren erabilera behin eta berriro errepikatuz gelditzen da, noiz gelditu jakin gabe.


## Ondorioak

Latxa VL beste urrats garrantzitsu bat da euskarazko adimen artifizialean. [Kimu](/blog/kimu) bezalako eredu txikiak lortzeaz gain, ikusmenerako gaitasuna duen eredua dugu orain; oso interesgarria izan daitekeena OCR moduko erabileran euskarazko dokumentuak digitalizatzeko eta bertatik informazioa modu egituratuan ateratzeko.