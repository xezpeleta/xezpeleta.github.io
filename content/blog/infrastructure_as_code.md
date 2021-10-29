---
title: "Infrastructure as code"
date: 2021-10-27T08:31:18+02:00
draft: true
---

Nire egunerokoan askotan erabili behar izaten ditut makina birtualak (VM). VMa sortu, sistema eragilea instalatu, konfiguratu, beharrezko dependentziak instalatu etab... askotan antzeko urratsak ematen ibiltzen naiz eta gainera, beti ahazten zait zeozer!

Gaur egun dauden automatizazio tresna ezberdinak erabiliz lan hauek murriztu ditzazkegu. Nire kasuan, helburu nagusia prozesu hau beti era berean egitea da (bidean ezer ahaztu gabe). Azken finean, **azpiegiturak kode bidez kudeatzerakoan gure lana autodokumentatzen ere ari garela uste dut**.

<!--more-->

Hurrengo artikuluetan VM sorrera eta software instalazioaren inguruko automatizazio gai hauek jorratzen saiatuko naiz:

- [**Cloud-Init**](https://cloud-init.io/): makina birtual baten hasieratzea kudeatzeko tresna da. Birtualizazio eta Cloud hornitzaile gehienek onartzen duten estandarra bihurtu da. Sistema eragilearen oinarrizko txantiloi bat izanda, hainbat konfigurazio ezarri daitezke aldiz aurretik (erabiltzaileak, sare konfigurazioa etab.)
- [**Terraform**](https://www.terraform.io/): _infrastructure as code (IaC)_ deritzon tresna ezaguna da. Cloud zerbitzuak sortu eta kudeatzeko balioko digu. Cloud hornitzaile ezberdinekin ulertzeko gaitasuna du (besteak beste, Proxmox) eta CloudInit konfigurazioak ere pasa ahalko dizkiogu.
- [**Ansible**](https://www.ansible.com/): software ezarketa eta konfigurazio kudeaketa automatizatua lortzeko tresna. Jadanik sortuta eta martxan dauden VMetara konektatu eta nahi dugun software eta konfigurazioak jartzeko erabiliko dugu.

Tresna bakoitzak funtzio zehatz bat du eta, hortaz, osagarriak dira.