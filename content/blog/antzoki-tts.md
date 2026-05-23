---
title: "Antzoki-TTS: emozio eta antzespen ahalmena gehituz"
date: 2026-05-16
draft: false
tags: ["ai", "euskara", "tts", "dramabox", "ltx2", "lora", "itzune", "openslr"]
cover:
    image: "/images/antzoki-tts-cover.png"
    alt: "Antzoki TTS"
    caption: "Antzoki TTS"
---

*Text-to-Speech* teknologia tradizionalak ahots sendoak ematen dizkigu gaur egun, baina ez du inolako aukerarik eskaintzen audioaren interpretazioa bideratzeko. Eredu hauek audioliburu bat, ipuin bat, jokoetarako audioak etab. sortzeko erabili nahi baditugu, laster konturatuko gara emaitzak ez direla aproposak. Ahots hotz eta neutralak lortuko ditugu. Robotikoak. Aspergarriak.

Azkenaldian, ordea, zeinu paralinguistikoak (etenak, arnasketak eta aldaera emozionalak) zehazteko aukera eskeintzen dizkiguten ereduak agertzen ari dira. Teknologia honi esker, gidoi motako aginduak emanez, **emozioz betetako ahots sintetikoak sortuko ditugu**.

Hain zuzen ere, [Antzoki-TTS](https://huggingface.co/itzune/antzoki-tts), nire azken esperimentuaren helburua horixe da: hiztunaren izaera, ezaugarri emozionalak eta paralinguistiko hauek definitu ahal izatea; eta **euskarazko emaitza txukunak** lortu ahal izatea.

Adibidez, honako agindua emanez gero (gidoi moduan, pertsonaia eta emozioak deskribatuz) maltzur baten ahots beldurgarri bat sor dezakegu, honako erreferentziak gidatuta:

> *A shadowy villain speaks with cold menace, "Nire lurretan sartu zara, morroi"
> He chuckles darkly, "Erruz ordainduko duzu."
> His voice rises with fury, "Belaunikatu, edo suntsituko zaitut!!"*

{{< rawhtml >}}
<audio controls preload="metadata">
  <source src="/audio/xabi_test_1.mp3" type="audio/mpeg">
  Zure nabigatzaileak ez du audio etiketa onartzen.
</audio>
{{< /rawhtml >}}

Edo, nahiago bada, neskato baten tonu gozo eta alaiagoa:

> *A bright-eyed girl spins in a field of wildflowers, her voice bubbling with pure, breathless wonder:
> "Aizu, aitona! Entzun duzu?!"
> She laughs, a sound as clear as a mountain stream.
> "Makina batek hitz egiten duela dirudi, baina hain da erreala!"
> She spreads her arms wide, looking up at the sky in disbelief.
> "Sinestezina da... adimen artifizialak nire ahotsa sortu du!!"*

{{< rawhtml >}}
<audio controls preload="metadata">
  <source src="/audio/xabi_test_2.mp3" type="audio/mpeg">
  Zure nabigatzaileak ez du audio etiketa onartzen.
</audio>
{{< /rawhtml >}}

**Antzoki-TTS** [DramaBox](https://www.resemble.ai/learn/models/dramabox) ereduan oinarrituta dago, zeina aldi berean [LTX-2](https://ltx.io/model/ltx-2) bideo ereduan oinarritua izan den. Izan ere, bideoak sortzeko eredu honetatik audioa eratzeko zatia erauzi dute eta emaitzak txundigarriak dira. Nire kasuan, jatorrizko ereduaren gainean [LoRA](https://huggingface.co/itzune/antzoki-tts) moldaketa bat entrenatu dut, euskararen ahoskera eta prosodia hobetzeko asmoz.

## Nola dabil?

*Zuzendari gidoi* motako testu-aginduaz gain, erreferentzia modura audio fitxategi bat emanez gero, honen ahots estiloa ere erabiliko du oinarri gisa. Hain zuzen ere horrela lortzen dira emaitza onenak.

Eredua bi elementu hauekin elikatzen da:

1. **Erreferentziazko audioa** (~10 segundo nahikoa, ahotsaren tinbrea eta estiloa kopiatzeko)
2. **Zuzendari gidoia**: testua ez ezik, interpretazioa ere deskribatzen duena (emozioak, pausak, arnasketak...)

Gidoiak ingelesera itzultzea gomendatzen dut, baina aipuen barruan doan testua euskaraz idazten da, eta emaitza ezin hobeto moldatzen da.

## Entrenamendua

Entrenamendurako [OpenSLR76](https://www.openslr.org/76/) datu-sorta erabili dut, euskaraz "ikas" dezan. Guztira 7.136 grabaketa, 52 hiztun ezberdinenak (29 emakumezko, 23 gizonezko), 14 ordu inguru osatzen dutenak.

Tamalez, datu-sorta honetan ahots neutralak besterik ez ditugu — irakurketa soilak — eta beraz antzezteko jatorrizko gaitasun hori pixka bat galdu duela ere esan genezake. Dena den, DramaBox-en oinarrizko eredua berez da oso adierazkorra, eta emaitzek oraindik ere kalitate handia dute.

## Erabilera

Eredua lokalean erabiltzeko, DramaBox instalatu behar da, eta ondoren LoRA kargatu `--lora` aukerarekin:

```bash
cd DramaBox
CUDA_VISIBLE_DEVICES=0 PYTHONPATH=ltx2 python src/inference.py \
  --checkpoint      dramabox-dit-v1.safetensors \
  --full-checkpoint dramabox-audio-components.safetensors \
  --lora            antzoki-tts/best_step_06850.safetensors \
  --voice-sample    erreferentzia.wav \
  --prompt          "Zure gidoia..." \
  --output          irteera.wav
```

Momentuz, behintzat, 12 GB VRAM inguru beharrezkoa da. Denborarekin, behar hauek ere jaitsiko direla ziur naiz, edonork bere ordenagailu arruntean exekutatzeko aukera izan arte.

## Mugak eta etorkizuna

Hemen argitaratu ditudan emaitza hauek, bereziki aukeratuta daude (*cherry picking*). Akatsak ere egiten ditu noizbehinka eta hobetzeko aukera asko ikusten dizkiot. Etorkizunari begira, datu adierazkorrarekin entrenatzeak (ipuin kontaketak, antzezpenak...) asko hobetuko lituzkeela uste dut. Teknikoki ez dirudi bereziki zaila, baina badira bestelako mugak (jabegotza eskubideak) erabilera mugatuko luketenak. 

[LoRA eredua eskuragarri dago Hugging Face-n](https://huggingface.co/itzune/antzoki-tts), [Itzune](https://huggingface.co/itzune) proiektuaren baitan. Animatu zaitezte probatzera!
