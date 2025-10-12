---
title: "Deseskalatzeko momentua iritsi al da?"
date: 2024-03-04
draft: true
tags: ["docker", "heroku", "kubernetes", "sablier"]
cover:
    image: "/images/cover_scale_to_zero.png"
    alt: "Scale-to-zero estrategia irudikatzeko kontzeptua"
    caption: "Scale-to-zero estrategia irudikatzeko kontzeptua (Gemini 2.5 Flash bidez sortua)"
---

Adimen artifizialak duen erronka handieneko bat beharrezko baliabideak dira. Zure erakundean, elkartean, ikastetxean, kooperatiban edo enpresan **eredu lokalak** erabiltzeko ideia izan baduzu, laster konturatuko zinen muga nagusiena zein den.

Izan ere, txat adimenduna, irudi sortzaile edota transkripzio automatikoak egiteko tresna bat ezarri nahi baduzu zerbitzu gisa, *hardware* berezia (garestia eta energia kontsumo handikoa) beharko duzu.

Adibide modura: demagun Latxa 70B bezalako hizkuntza eredu bat ezarri nahi duzula eta hainbat erabiltzaileren esku utzi erabil dezaten. Horretarako, XXX GB memoria dituen *GPU* (txartel grafiko) bat beharko genuke. Eta noski, txartel hori aproposa den zerbitzari batean jarri beharko dugu. Guztira XXX € -ko inbertsioaz ariko ginateke eta XXX Kwh-ko.

> Okerrena da zerbitzua eskuragarri uzteko, aplikazioa martxan jarri bezain laster baliabideak jadanik erreserbatuak gelditzen direla, erantzun azkar bat eman ahal izateko. Beraz, nahiz eta erabiltzailerik ez egon, baliabide hauek jadanik okupatuta izango ditugu.

Eta orain, **Flux** irudi sortzailea **ere** eskeini nahiko bagenu? Edo bideo sortzailea? Edo *text-to-speech (TTS)* egiteko aukera?

Kasu horretan bi aukera izango genituzke:

- Baliabide gehiago eskuratu: *GPU* berri bat (diru gehiago, kontsumo gehiago...)
- Zerbitzu bat itzali, bestea martxan jartzeko

Zerbitzu bat itzali? Bainan erabiltzaileek ez al dute ba suposatuko zerbitzua beti eskuragarri egongo dela *24x7*?

Itxaron, itxaron. Horrelako etenaldiak automatizatzeko aukera izango bagenu? Eta erabiltzaile bat konektatzen denean zerbitzua martxan jarriko bagenu?

Hain zuzen, **"_Scale-to-zero_**" estrategiak hau bilatzen du: zure zerbitzuak, eskeintzeko beharrezko baliabideak zerora eskalatzeko gai izatea (erabiltzen ez direnean).

Horren adibide da, adibidez, [Sablier](https://github.com/sablierapp/sablier) tresna. Beharrezkoa denean, zure *Docker* edukiontzia altxatuko du eta aplikazioa eskuragarri jarriko da. Aktibitate gabeko denbora bat pasa ondoren, automatikoki itzaliko da. Duela urte batzuk gutako askok erabiltzen genuen *Heroku* zerbitzu hura bezalaxe, bainan software askean eta guk geuk eskeinita!

Har dezagun adimen artifizialaren olatua, baina beti ere ikuspuntu arduratsu eta jasangarri batetik. Alderatu ditzagun onurak eta desabantailak. Eta beharrezkoa ikusten badugu, bilatu dezagun hauek ezartzeko modu jasangarri bat.