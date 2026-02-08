---
title: "New Latxa VL Models"
date: 2026-02-07
draft: false
tags: ["llm", "hitz", "ai", "qwen", "basque models"]
cover:
    image: "/images/latxa-vl-cover.png"
    alt: "Latxa VL model"
    caption: "Latxa VL"
---

Recently, the HiTZ center published the [Latxa VL](https://huggingface.co/collections/HiTZ/latxa-vl) models. These models are based on Qwen3-VL models and possess vision capabilities.

Currently, two sizes are available, both very small: models with 2B and 4B parameters. The tests presented below were performed with the 4B model.

## Models that know Basque

Generally, models of such small size tend to only have the ability to answer decently in English. These Latxa VL models, however, have been trained to perform in Basque.

![Latxa-VL greeting](/images/latxa-vl-agurra.png)

Although capable of understanding Basque, it often makes some mistakes in its responses.

![Latxa-VL question answering](/images/latxa-vl-galdera.png)

## Ability to understand images

The uniqueness of this type of VL models is their vision capability. In this case, moreover, we can see that it is capable of taking the request in Basque and answering in Basque.

![Latxa-VL describing an image](/images/latxa-vl-porrotx.png)

As in the previous example, we can use it to describe images, although a lack of precision is noticeable in many cases.

However, like the parent Qwen3-VL model, Latxa VL is excellent for use as OCR. That is, extracting text present in an image.

![Latxa-VL as OCR](/images/latxa-vl-ticket.png)

In this case, I gave it a photo of a ticket and asked it to give me all the information from it.

![Ticket demo](/images/ticket_demo.jpeg)

This was its response:

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

As you can see, it is able to extract most of the information from it, with almost no errors. I would also say that it has a better ability to extract texts in Basque compared to Qwen3-VL models. Although to certify this, we would need a more detailed evaluation.

## Structured Output

Another interesting feature of these new models published in the last year is the ability to generate structured output. That is, we can obtain outputs with a CSV table or JSON structure to answer our requests in a specific way.

Thanks to this, we can integrate these models into automation workflows. For example, if we wanted to pass images of tickets and always obtain detailed information from them in the same way, we could use the following n8n automation.

![latxa-vl model in an n8n automation](/images/latxa-vl-n8n.png)

![structured output thanks to latxa-vl model](/images/latxa-vl-n8n-2.png)


## Tool Usage

Structured output facilitates the use of tools. Thus, we can configure an MCP server in our AI agent and make its tools available to the model to use when needed.

I have verified that it calls these tools correctly but, unfortunately, in the tests I have done, the tool usage gets stuck repeating itself over and over again, without knowing when to stop.


## Models available in GGUF format

I have converted the Latxa VL models to GGUF format and made them available in the [**Itzune** initiative space](https://huggingface.co/collections/itzune/latxa-vl-gguf) on HuggingFace.


## Conclusions

Latxa VL is another important step in Basque artificial intelligence. It may not perform as well as [Kimu](/blog/kimu) in Basque, probably because its size is also smaller.

On the other hand, it should be emphasized that we now have a model with vision capability; which can be particularly interesting for uses like OCR to digitize Basque documents and extract information from them in a structured way.

However, we face several challenges in the future. Such as making these small-sized models perform better in Basque.
