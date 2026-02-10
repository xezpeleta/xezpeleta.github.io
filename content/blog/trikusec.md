---
title: "TrikuSec"
date: 2026-02-10
draft: false
tags: ["segurtasuna", "lynis", "linux", "auditoria", "kode irekia", "docker"]
cover:
    image: "/images/trikusec-cover.png"
    alt: "TrikuSec Azala"
    caption: "TrikuSec Azala"
---

[Lynis](https://cisofy.com/lynis/) kode irekiko segurtasun-auditoria tresna bat da, Linux sistemetarako pentsatua. Fitxategi baimenak, kernel parametroak, instalatutako paketeak, martxan dauden zerbitzuak eta gehiago eskaneatzen ditu. Irakurketa hutsekoa da; ez du sisteman ezer aldatzen, aurkitzen duena soilik ematen du jakitera.

Arazoa zerbitzari anitz kudeatu behar direnean sortzen da. Lynis bakoitzean exekutatzea, txostenak biltzea eta denboran zehar aldaketak jarraitzea neketsua bihurtzen da.

## Lynis-entzako aginte-panel zentralizatua

![TrikuSec Devices Dashboard](https://raw.githubusercontent.com/trikusec/trikusec/main/docs/assets/img/trikusec-devices.png)

Hau konpontzeko **TrikuSec** sortu dut. Plataforma zentralizatu bat da, zerbitzari anitzetatik Lynis auditoria-txostenak biltzen dituena eta web aginte-panel bakar batean aurkezten dituena.

Nola funtzionatzen du:

1. TrikuSec Docker bidez zabaldu (`docker compose up -d`)
2. Zerbitzari bakoitza konfiguratu Lynis txostenak cron lan baten bidez bidaltzeko
3. Emaitza guztiak aginte-paneletik ikusi

Lynis-ek bezala, TrikuSec-ek **irakurketa hutseko** eredua jarraitzen du. Zerbitzariek datuak bidaltzen dizkiote TrikuSec-i, baina TrikuSec-ek ez du inoiz agindurik bidaltzen bueltan.

## Ezaugarri nagusiak

- **Gailuen Kudeaketa**: Zerbitzari guztien egoera arakatu leku bekarretik, hostname, sistema eragile eta banaketa bezalako metadatuen bidez.
- **Betetze Politikak**: Arauak definitu (adibidez, "SSH root sarbidea desgaituta egon behar da") eta egiaztatu zerbitzari guztiak automatikoki haien aurka.

![TrikuSec Policies](https://raw.githubusercontent.com/trikusec/trikusec/main/docs/assets/img/trikusec-policies.png)

- **Aldaketen Jarraipena**: Auditorien arteko txostenak alderatzen dira, zehazki zer aldatu den ikusteko.
- **PDF Txostenak**: Dokumentazio edo auditorietarako betetze-egoera esportatu.

## Hurrengo urratsak

Etorkizuneko bertsioetarako ideia batzuk baditut dagoeneko: *dashboard* bat grafiko interaktibo eta joeren analisiarekin, alerta-sistema bat betetze-aldaketetarako, eta agian Windows zerbitzarietatik txostenak jasotzeko aukera.

## Probatu

TrikuSec kode irekikoa da GPL-3.0 lizentziapean.

- Iturburu kodea: [github.com/trikusec/trikusec](https://github.com/trikusec/trikusec)
- Dokumentazioa: [trikusec.github.io/trikusec](https://trikusec.github.io/trikusec/)

```bash
docker compose up -d
```

**Garrantzitsua**: TrikuSec ez da produktu profesionala, garapen aktiboan dagoen kode irekiko proiektua baizik. Enpresa mailako laguntza eta SLA-ak behar badituzu, kontuan hartu CISOfy-ren [Lynis Enterprise](https://cisofy.com/pricing/).

> Oharra: Ez dut loturarik CISOfy-rekin ezta Lynis proiektuarekin ere.
