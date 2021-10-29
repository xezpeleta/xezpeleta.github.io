---
title: "Traefik"
date: 2021-10-27T13:14:35+02:00
draft: true
---

Traefik _load balancer_ eta _reverse proxy_ ezagun bat da. Modan jarri da azken urteetan kontainerizazioaren olatua dela eta. Izan ere, edukiontzien ingurunean horrelako tresnak ezinbestekoak dira.

<!--more-->

## Zertarako da _reverse proxy_ bat?

Batzuetan IP publiko bakar baten bidez web zerbitzari ezberdinetara bideratzea behar izaten dugu. Hori da hain zuzen ere _"reverse proxy"_ baten lana.

Zertarako beharko genuke horrelako bat? Erabilera kasu ezberdinak daude
- IP publikoak aurreztea
- Konexioak orekatzea
- Web trafiko guztia aztertu ahal izateko
- SSL zertifikatuen kudeaketa zentralizatzeko
- Atzipen URLa moldatzea

## Traefkik