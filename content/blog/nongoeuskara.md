---
title: "Euskalkiak identifikatzen"
date: 2026-06-28
draft: false
tags: ["ai", "euskara", "euskalkiak", "dialect", "fasttext", "autoreserch"]
---

## DR;TL ("Ez dut irakurri; luzeegia" bertsioa)

[NongoEuskara](https://itzune.eus/nongoeuskara/) esperimentua sortu dut. Horretarako, datuak bilatu, *fastText* saikapen edo *embedding* eredua entrenatu, eta demo webgunetxo hau sortu dut. *WebAssembly* erabiliz, eredu hauek nabigatzailean exekutatzen dira.

## Azalpen luzea

Badakigu hizkuntza eredu handiak (LLM) denetik egiteko gai direla. Nahiz eta, hasiera batean, ez ziren horretarako sortu, gaur egun gai dira programatzeko, itzulketak egiteko, audioa transkribatzeko, testu luzeak laburtzeko, etabar luze bat. Batzuetan, ordea, soluzio egokiena ez da beti LLM bat erabiltzea izango. Adibidez, itzulpen azkarrak eta sinpleak egiteko, badira LLMak baino itzultzaile neuronal arinagoak, baliabide gutxiago behar dituztenak.

Hizkuntza identifikatzaileekin antzerakoa gertatzen da. Testu bat emanda, zein hizkuntza den jakiteko, ez dugu LLM baten beharrik. [**Hizkuntzaren Identifikazioa**](https://eu.wikipedia.org/wiki/Hizkuntzaren_identifikazioa) horretaz arduratzen da hain zuzen. [fastText](https://fasttext.cc/) (Meta AI) bezalako *embedding* ereduak horretarako balio dezakete besteak beste. Badaude jadanik entrenatutako ereduak, baliabide gutxirekin, hizkuntza identifikatzeko gai direnak.


## Eta euskalkiak identifikatzeko?

Galdera honi erantzun nahian, ideiarik izan gabe, eskura ditugun aukerak aztertzen hasi nintzen. Nahiz eta ez dudan aurkitu ezer honen inguruan argitaratuta, pentsatzen dut etxeko lan edo gradu amaierako lanen batean ikasleek egingo zituztela honekin haien esperimentuak.

Nik **fastText** liburutegia erabiliz [sailkapenerako ereduak sortu ditut euskalkiak identifikatzeko](https://huggingface.co/itzune/zeineuski). Eredu hauek edozein gailu xumeetan exekutatu daitezke. Hare gehiago, eredua *entrenatzeko* ere ez dut *GPU* edo ordenagailu berezirik behar izan.

Lan gehiena, datuak eskuratzea izan da. Horretarako, bereziki eskertu nahiko nituzke erabili ditudan iturriak: [Ahotsak.eus](https://ahotsak.eus), [Euskalkien Katalogoa (HiTZ)](https://github.com/hitz-zentroa/Catalog-of-Basque-Dialects), [Klasikoak (Armiarma)](https://klasikoak.armiarma.eus/) eta desagertutako [SÜ AZIA](https://web.archive.org/web/20110920103304/http://www.suazia.com).

## Autoresearch

Gauza da, lehen esan bezala, nik honi buruz ez dakidala gauza askorik. Bereziki, ereduak entrenatzea, emaitzak interpretatzea, etab. lan handia da eta ezagutza espezifikoak behar dira. Lan hau errezteko [pi-autoresearch](https://github.com/davebcn87/pi-autoresearch) erabili dut. Entrenamenduak eta hauen emaitzak optimizatzeko bereziki sortutako agente-extentsio bat da.

Modu laburrean azalduta: entrenamendu hiperparametro edo konfigurazio ezberdinak probatzen joango da, beti ere aurretik jasotako emaitzen interpretazioaren baitan, behin eta berriro (nekaezina da). Emaitzak hobetzea lortu badu, aldaketak gordeko ditu. Kaxkarragoak badira, ezeztatzen dira. Horrela, behin eta berriro, 30 bat saiakera egin eta emaitzak ikaragarri pila hobetu dituela ikusi dut.

Emaitzak kuantitatiboki neurtzeko errezak direnean, interesgarria izan daiteken fluxua iruditu zait. Kasu oso zehatzetarako. Bestalde, bere buruari tranpak egiten hastea oso posible dela ere konturatu naiz.

## Nongo euskara ?

Eredu hauekin zer egin, eta demo txukun bat egin behar zela pentsatu nuen. Dena web estatiko baten bidez, ahal bada, mantenua errezteko eta dohainezko baliabideak aprobetxatzeko.

Erabiltzaileak testu bat sartu, identifikatu eta Euskal Herriko mapan azpieuskalkia eta dagokion eskualde multzoa azpimarratzea nahi nuen. **Spoiler:** nola ez, *frontend* zati hau izan da gehien kostatu zaidan zatia! Entrenamendua baina gehiago!

Hau egiteko, *WebAssembly* (*WASM*) bidez exekutatu behar izan dut eredua, aldez aurretik *kuantizatuta* (konprimatuta). Berirro ere ondorio berdina: *WASM* ikaragarria da horrelako gauzetarako! Zerbitzaririk gabe, datuak inora bidali gabe, erabiltzaileok gure nabigatzaileetan punta-puntako aplikazio edo adimen artifizialeko ereduak exekutatu ditzakegu.
