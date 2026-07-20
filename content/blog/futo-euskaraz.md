---
title: "Euskarazko testu prediktiboa mugikorretan pribatutasuna errespetatuz"
date: 2026-07-20
draft: false
tags: ["ai", "euskara", "autocompletion", "gboard", "transformer", "llama", "latxa", "futo", "auto-osaketa"]
---


## TL;DR (Luzeegia; Ez Dut Irakurri)

Android-en euskarazko testu prediktiboa izateko hizkuntza eredu txiki bat entrenatu dut. [**FUTO Keyboard**](https://keyboard.futo.tech/)-ekin erabili daiteke telefonoan. Google-en *Gboard* ezagunaren antzera, hurrengo hitza aurreikusteko eta akatsak zuzentzeko gaitasuna du.

## Auto-osaketaren inguruan

Auto-osaketa eta antzeko idazketarako laguntza teknologiak ez dira berriak. Aspalditik daude gurekin. Azken urteetan, ordea, adimen artifizialak bultzaturik, aurrera-pauso handiak eman dira. Hauek dira, gaur egun eskura ditugun aukera nagusiak:

- **Hiztegi bidezko hitz-osaketa**: auto-osaketaren forma klasikoena eta oinarrizkoena da. Erabiltzaileak "ira" idazten duenean, hiztegian berdin hasten diren hitzak bilatu eta "iragana" edo "irabazi" proposatuko zaizkio. Gainera, gehien erabilitako hitzak lehenetsi daitezke bereziki.
- **Zuzenketa automatikoa**: oinarrizkoa (hiztegi bidezkoa) hala aurreratua; testuinguru osoa ulertuz akatsak detektatu eta zuzentzeko gai dena.
- **Testuinguru-osaketa**: Idatzitako mezu guztia (edo zati handi bat) erabiliz hurrengo hitza (edo hitzak) asmatzeko gaitasuna da. Kasurik onenean, esaldi berria idazten hasi gabe ere, asmatzeko gai izan daiteke!
## Hemen ere, Google nagusi

Google aintzindari izan zen, bere *Gboard* teklatuan hizkuntza anitzetan teknologia hauek txertatzen. Baina, nola demontre da gai buruan dudan hitza asmatzeko?

Sekretua mugikorrean bertan gorde eta exekutatzen duen hizkuntza eredu txiki batean dago. *LSTM* arkitekturako eredu txiki hau, [*Federated Learning*](https://en.wikipedia.org/wiki/Federated_learning) bidez entrenatzen da, milioika erabiltzaileren laguntzaz.

> *Gboard*  erabiltzen duzu? Bazenekien zure mugikorra gau erdian esnatu eta ikasitako hitz berriak beste milioika mugikorrekin partekatzen dituela?

Asmakizun paregabea da. Eta, diotenez, [pribatutasuna errespetatuz egiten dute](https://arxiv.org/abs/2305.18465) hau guztia. Baina, nola jakin zehazki horrela dela? Kodea eskura izan gabe eta aztertzeko aukerarik gabe, ziur egon al gaitezke Googlek esaten duena egiten duela?

## FUTO keyboard, alternatiba "irekia"

Android sakeleko alternatiba ezagunenetariko bat, [**FUTO Keyboard**](https://keyboard.futo.tech/) teklatua da, pribatutasuna du ezaugarri nagusietako bat.

Hiztegi bidezko ohiko hitz-osaketaz gain, [*Transformers* arkitekturan oinarritutako eredu txiki bat erabiltzeko aukera eskaintzen du](https://docs.keyboard.futo.tech/settings/textprediction), auto-osaketarako eta baita zuzenketarako ere. Tamalez **ingelesezko eredua bakarrik** eskaintzen du proiektuak. Baina nahi izanez gero, beste edozein eredu aukeratu dezakegu modu errazean.

## Eta euskarazko *Transformers* eredu bat sortzen badugu?

Beraz, Euskaraz hurrengo hitza zein den iragartzeko gaitasun aurreratua nahi badugu, gure *Transformer*  eredua behar dugu. Gai hauen inguruan ikasten eta esperimentuak egiten ibili naiz hain zuzen azken egunetan (laster gehiago honen inguruan). Eta ikasitakoa praktikan jartzen hasi eta.. sorpresa! badabilela dirudi!

Xehetasun guztiak [FUTO-Basque proiektuaren webgunean](https://github.com/itzune/futo-basque) aurkituko dituzue. [Latxa Corpus v2](https://huggingface.co/datasets/HiTZ/latxa-corpus-v2) datu-sorta (zati bat) erabili dut entrenamendurako.

Eredu hau gehitzean, euskarazko hurrengo hitz proposamenak eskainiko dizkigu, guk aurretik idatzitako testuaren arabera.

![Hurrengo hitzaren iragarpenak FUTO teklatuan, euskaraz idatzi ahala.](/images/futo-next-word.gif)

Eta akatsak ere automatikoki zuzentzen laguntzen digu:

![Akatsen zuzenketa automatikoa euskaraz FUTO teklatuarekin.](/images/futo-correction.gif)

## Nola instalatu FUTO euskarazko iragarpenekin?

1. [*FUTO Keyboard* instalatu](https://keyboard.futo.tech/#download), nahi duzun erara (*Play Store* edo *F-Droid* bidez).
2. Gehitu teklatu konfigurazio eta hizkuntza bat (gutxienez):
	 - Mota: *QWERTY +1* 
	 - Hizkuntza: Euskara
	 - Hiztegia: aukeratu [euskarazko hiztegia](https://keyboard.futo.tech/dictionaries?locale=eu-ES)
3. Deskargatu [Futo-Basque proiektuko eredua *Release* ataletik](https://github.com/itzune/futo-basque/releases/download/v2.0.0/eu_futo_v2.gguf) zure telefonoan (*.gguf* fitxategi bat da, 48MB ingurukoa)
4. Inportatu euskarazko eredua:
	 - *Settings* > *Languages & Models* > *Import model* (aukeratu aurreko urratsean deskargatutako gguf fitxategia)

## Eta hizkuntza bat baina gehiago nahasten ditugunean?

Kezka ohikoa da hiztun eleanitzontzat. Beti baikabiltza hizkuntza ezberdinak nahasten, elkarrizketa berdinean ere.

Horrelako kasuetarako [ezarpen berezi bat](https://docs.keyboard.futo.tech/settings/languagesmodels#enable-multilingual-typing) eskaintzen du FUTOk. Gehitu erabili nahi dituzuen hizkuntzak, bakoitza bere hiztegi eta ezarpenekin, eta aktibatu "*Multilingual typing*" aukera  nahastu nahi dituzun hizkuntza guztietan.

!["Multilingual typing" aukera aktibatuta, hizkuntza ezberdinak nahasteko.](/images/futo-multilingual.jpg)

Honi esker, hizkuntzak aldatzen ibili behar gabe, testu-osaketa eta zuzenketa bezalako ezaugarriak erabilgarri egongo dira hizkuntza ezberdinetan.

## Euskara hizkuntza handienen pare

Bada [hari bat FUTOren GitHub webgunean](https://github.com/futo-org/android-keyboard/issues/1212) gai honi buruz hitzegiten: askok nahi dute haien hizkuntzan hurrengo hitza osatzeko gaitasuna. Frantsesa, greziera, norvegiera, suediera edota turkiera eskatzen dabiltza eta itxaroten. Momentuz, ingelerazko eredu ofizialaz gain, nik dakidala gutxi batzuk daude eskuragarri: portugesa eta poloniera. Eta orain, euskarazkoa!


> FUTOk *"FUTO Source First License"* lizentzia propioa erabiltzen du. Kodea eskuragarri eta aldatzeko aukerarekin uzten du, baina muga batzuekin. Besteak beste, erabilera komertziala ez da onartzen.
>
>Hau dela eta, OSI (Open Source Initiative) edo FSF (Free Software Foundation) bezalako erakundeen arabera **FUTOk ez ditu software-aske gisa izendatzeko baldintzak betetzen**.
