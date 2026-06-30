---
title: "Euskalkiak identifikatzen"
date: 2026-06-28
draft: false
tags: ["ai", "euskara", "euskalkiak", "dialect", "fasttext", "autoreserch", "webassembly", "wasm"]
---

## TL;DR ("Luzeegia; ez dut irakurri" bertsioa)

[NongoEuskara](https://itzune.eus/nongoeuskara/) esperimentua sortu dut, testu bat emanda zein euskalkitan idatzia den jakiteko. Horretarako, datuak bilatu, *fastText* saikapen edo *embedding* eredua entrenatu, eta demo webgunetxo hau sortu dut. *WebAssembly* erabiliz, [sortutako eredu hauek](https://huggingface.co/itzune/zeineuski) nabigatzailean exekutatzen dira.

## Azalpen luzea

Badakigu hizkuntza eredu handiak (LLM) denetik egiteko gai direla. Nahiz eta, hasiera batean, ez ziren horretarako sortu, gaur egun gai dira programatzeko, itzulketak egiteko, audioa transkribatzeko, testu luzeak laburtzeko, etabar luze bat. Batzuetan, ordea, soluzio egokiena ez da beti LLM bat erabiltzea izango. Adibidez, itzulpen azkarrak eta sinpleak egiteko, badira LLMak baino itzultzaile neuronal arinagoak, baliabide gutxiago behar dituztenak.

Hizkuntza identifikatzaileekin antzerakoa gertatzen da. Testu bat emanda, zein hizkuntza den jakiteko, ez dugu LLM baten beharrik. [**Hizkuntzaren Identifikazioa**](https://eu.wikipedia.org/wiki/Hizkuntzaren_identifikazioa) horretaz arduratzen da hain zuzen. [fastText](https://fasttext.cc/) (Meta AI) bezalako *embedding* ereduak horretarako balio dezakete besteak beste. Badaude entrenatutako *fastText* ereduak eskuragarri hizkuntzak identifikatzeko, exekutatzeko konputazio baliabide gutxi behar dituztenak.


## Eta euskalkiak identifikatzeko?

Galdera honi erantzun nahian, gaiari buruzko ezagutzarik gabe, eskura dauden aukerak aztertzen hasi nintzen. Nahiz eta ez dudan aurkitu ezer honen inguruan argitaratuta, pentsatzen dut etxeko lan edo gradu amaierako lanetan, ikasle batek baina gehiagok sortuko zituela euskalkiak identifikatzeko sistemak (sare neuronalak edo bestela oinarrizko erregela bidezkoak).

Azkenean, **fastText** liburutegia erabiliz [euskalkiak identifikatzeko sailkapen-ereduak sortu ditut](https://huggingface.co/itzune/zeineuski). Eredu hauek edozein gailu xumeetan exekutatu daitezke. Are gehiago, eredua *entrenatzeko* ere ez dut *GPU* edo ordenagailu berezirik behar izan.

Lan mardulena, datuak eskuratzea izan da. Horretarako, bereziki eskertu nahiko nituzke erabili ditudan iturriak: [Ahotsak.eus](https://ahotsak.eus), [Euskalkien Katalogoa (HiTZ)](https://github.com/hitz-zentroa/Catalog-of-Basque-Dialects), [Klasikoak (Armiarma)](https://klasikoak.armiarma.eus/) eta desagertutako [SÜ AZIA](https://web.archive.org/web/20110920103304/http://www.suazia.com).

## Autoresearch

![NongoEuskara pi-autoresearch pantaila-argazkia](/images/pi_autoresearch_zeineuski.png)

Gauza da, lehen esan bezala, ez naizela aditua esparru honetan. Ereduak entrenatzea, emaitzak interpretatzea, etab. lan handia da eta horretarako ezagutza espezifikoak behar dira. Lan hau errezteko [pi-autoresearch](https://github.com/davebcn87/pi-autoresearch) erabili dut. Entrenamenduak eta hauen emaitzak optimizatzeko bereziki sortutako agente-extentsio bat da.

> Modu laburrean azalduta: entrenamendu hiperparametro edo konfigurazio ezberdinak probatzen joango da, beti ere aurretik jasotako emaitzen interpretazioaren baitan, behin eta berriro (nekaezina da). Emaitzak hobetzea lortu badu, aldaketak gordeko ditu. Kaxkarragoak badira, ezeztatzen dira. Horrela, behin eta berriro, 30 bat saiakera egin eta emaitzak ikaragarri pila hobetu dituela ikusi dut.

Ondorio gisa: emaitzak kuantitatiboki neurtzea posible denean, interesgarria izan daiteken fluxua iruditu zait. Kasu oso zehatzetarako soilik. Bestalde, kontuz gainbegiratu beharrekoa, bere buruari tranpak egiten hastea oso posible dela ere konturatu naiz.

## Nongo euskara ?

Eredu hauekin zer egin, eta demo txukun bat egin behar zela pentsatu nuen. Web estatiko baten bidez, ahal bada, mantenua errezteko eta dohainezko baliabideak aprobetxatzeko.

Erabiltzaileak testu bat sartu, identifikatu eta Euskal Herriko mapan azpieuskalkia eta dagokion eskualde multzoa azpimarratzea nahi nuen. **Spoiler:** nola ez, *frontend* zati hau izan da gehien kostatu zaidan zatia! Entrenamendua baina gehiago!

Hau egiteko, *WebAssembly* (*WASM*) bidez exekutatu behar izan dut eredua, aldez aurretik *kuantizatuta* (konprimatuta). Ondorio gisa: **_WASM_** ikaragarria da horrelako gauzetarako! Zerbitzaririk gabe, datuak inora bidali gabe, erabiltzaileok gure nabigatzaileetan punta-puntako aplikazio edo adimen artifizialeko ereduak exekutatu ditzakegu.
