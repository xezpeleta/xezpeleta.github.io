---
title: "Euskarazko ahots sintesirako eredu berriak: Maider, Antton eta OmniVoice"
date: 2026-04-04
draft: false
tags: ["ai", "euskara", "tts", "hitz", "aholab", "itzune", "pipertts", "omnivoice", "xiamoi"]
---

Azken urteetan testutik hizketara (ingelesez *Text-To-Speech* edo *TTS*) bihurtzeko ereduak izugarri garatu dira. Hilabetez-hilabete ahoskera, prosodia edota audioaren kalitatea hobetzen zuten ereduak argitaratu dituzte. Tamalez, haietako gehienak ingelesez egiteko prestatuak edota, kasurik hoberenean, hizkuntza gutxi batzuekin bateragarriak.

Euskarazko ahotsak sortzeko eskuragarri genituen tresnak mugatuak ziren; ordainezko sistema propietarioak (Orai-k garatutako [Elhuyarren TTS neuronala](https://ttsneuronala.elhuyar.eus/) ) edo, bestela, nabarmen atzean geldituak ziren ahots robotiko horiek...

Zorionez, panorama aldatzen ari da azken hilabeteetan.

## *Maider* eta *Antton*, HiTZ zentroak argitaratutako ereduak

[HiTZ zentroak bere TTS ereduak argitaratu ditu](https://huggingface.co/collections/HiTZ/tts). ILENIA proiektuaren baitan argitaratutako bi ahots argitaratu dituzte: Antton (gizonezkoa) eta Maider (emakumezkoa). Eredu hauek eskuragarri daude bakoitzak bere ordenagailuan exekutatu ahal izateko, edota nahiago bada, [Aholab-en webgunearen bidez](https://aholab.ehu.eus/DNN/TTS/) erabili daitezke ezer instalatu gabe.


{{< rawhtml >}}
<audio controls preload="metadata">
  <source src="/audio/tts_aholab_maider_demo.mp3" type="audio/mpeg">
  Zure nabigatzaileak ez du audio etiketa onartzen.
</audio>
{{< /rawhtml >}}


## Piper TTS euskarazko ahotsak

Hain zuzen ere, HiTZ zentroak argitaratutako bi ahots horiek baliatuz, [Urtzi Odriozolak Piper TTS-rako egokitu ditu](https://blogak.eus/urtzai/maider-eta-antton-euskarazko-tts-ahotsak-piper-motorrerako-egokitu-ditut). [Piper TTS](https://github.com/OHF-Voice/piper1-gpl) testutik hizketara bihurtzeko tresna arina eta azkarra da. Honi esker, ahots sintetikoak sortu ditzakegu gure gailu xumeetan oso modu azkarrean.

Nahi izanez gero, ezer instalatu gae, [ahots hauek lokalean sintetizatu ahal izateko webgunea sortu dut](https://itzune.github.io/basque-piper-tts/) WebAssembly bidez.


{{< rawhtml >}}
<audio controls preload="metadata">
  <source src="/audio/tts_itzunepiper_demo.mp3" type="audio/mpeg">
  Zure nabigatzaileak ez du audio etiketa onartzen.
</audio>
{{< /rawhtml >}}

## OmniVoice (Xiaomi)

Azken urteetan ezagun egin diren TTS eredu ezagunenak ([Coqui](https://github.com/coqui-ai/tts), [Kokoro](https://huggingface.co/hexgrad/Kokoro-82M), [StyleTTS2](https://styletts2.github.io/), [VibeVoice](https://github.com/microsoft/VibeVoice), ...) badituzte hainbat ezaugarri amankomunean:

- **Ahotsak klonatzeko aukera**: sarrera gisa, testuaz gain, erreferentzizko ahots grabaketa labur bat eskeini eta emaitza ahots hori erabiliz sortuko da
- **Emozioen kontrola**: barrea, harridura, hasperena... bezalako espresioak sortzeko aukera, etiketa bidez

Eta noski, ahots "errealagoak", grabaketa erreal batetik ozta-ozta ezberdindu daitezkenak.

Ba, sorpresa! justu ezaugarri guzti hauek betetzen dituen eredu berri bat argitaratu du *Xiaomi Corp.* erraldoiak: [**OmniVoice**, 600 hizkuntza baina gehiago sintetizatzeko gai den eredua](https://github.com/k2-fsa/OmniVoice).

{{< rawhtml >}}
<audio controls preload="metadata">
  <source src="/audio/omnivoice_demo.mp3" type="audio/mpeg">
  Zure nabigatzaileak ez du audio etiketa onartzen.
</audio>
{{< /rawhtml >}}

Egin ditudan proben arabera, euskaraz bikain egiten duela iruditzen zait, naturaltasun handiarekin. Sentimenduen kontrola egiteko aukera du, adibidez testuan *[laugher]* etiketa gehituta barrea txertatu nahi badiogu. Hain justu sentimendu kontrol hau euskaraz behintzat ez dabil oso fin, baina beno, ez gara kexatuko. Urrats garrantzitsu bat dela iruditu zait.

{{< rawhtml >}}
<audio controls preload="metadata">
  <source src="/audio/omnivoice_demo_tag.mp3" type="audio/mpeg">
  Zure nabigatzaileak ez du audio etiketa onartzen.
</audio>
{{< /rawhtml >}}

Bestalde, nahiz eta ordenagailu soil batean exekutatu daiteken, exekuzioa nahiko astuna eta motela da. Hitz gutxiko esaldi sinple batetik audioa sortzeko 5 minutu inguru behar ditu. Beraz, seguraski, horrelako ereduen inferentzia GPUa duten ordenagailu edo zerbitzarietan egitea izango da arruntena.

## Ondorio gisa

Bapateko sintesia behar dugunean, edozein gailutan lokalean exekutatzeko, euskarazko Piper TTS ereduak erabilgarri ditugu orain. [Euskarazko Parakeet] ahots errekonozimendu ereduarekin primeran moldatzen den eredua izan daiteke.

Aldiz, kalitate handiko euskarazko ahotsak sortu behar ditugunean, emaitzaren kontrol handiagoarekin, **OmniVoice** aukera interesgarria izan daitekela iruditzen zait. Hori bai, horretarako GPU txartela duen ordenagailua edo zerbitzaria beharko dugu.
