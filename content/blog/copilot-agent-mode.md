---
title: "GitHub Copilot Agent Mode: Garapenerako lankide adimenduna"
date: 2024-03-26
draft: false
tags: ["github", "ai", "vscode"]
cover:
    image: "/images/copilot-agent-mode.png"
    alt: "GitHub Copilot Agent Mode"
    caption: "The agent awakens"
---

GitHub Copilot-ek aurrerapen garrantzitsu bat ekarri du: [Agent Mode](https://github.blog/news-insights/product-news/github-copilot-the-agent-awakens/) delakoa. Ezaugarri berri honekin, VS Code editoreko testu interfazea erabiliz, zure proiektuko fitxategiak aztertu, aldatu eta exekutatu ditzake modu autonomoan.

## Zer da Agent Mode edo SWE agent delakoa?

Agent Mode-k GitHub Copilot-en gaitasunak zabaltzen ditu, kode osatzaile soil bat izatetik garapen laguntzaile autonomo bat izatera pasatuz. Adimen artifizialak proiektuko fitxategiak aztertu, ulertu eta aldatu ditzake, eta baita terminaleko komandoak exekutatu ere.

## Nola funtzionatzen du?

Agent Mode-k gaitasun bereziak ditu bere kodea hobetzeko eta erroreak konpontzeko. Bere proposamenak behin eta berriz birfindu ditzake, erroreak identifikatu eta automatikoki konpondu. Terminal komandoak iradoki eta exekutatzeko gai da, eta exekuzio-denborako erroreak aztertu eta konpondu ditzake.

> *Eta zuk eskatutako ataza osatu arte jarraituko du lanean. Eskatutako ataza soila egin beharrean, orain gai da zehaztu ez diren baina beharrezkoak diren ataza osagarriak inferitzeko. Are gehiago, bere erroreak detektatu ditzake, terminaleko mezuak chat-era kopiatu/itsatsi behar izan gabe.*

Agent moduan, Copilot ez da mugatzen soilik bere irteera hobetzera; irteera horren emaitzak ere aztertzen ditu. Eta zuk eskatutako ataza osatu arte jarraituko du lanean. Eskatutako ataza soila egin beharrean, orain gai da zehaztu ez diren baina beharrezkoak diren ataza osagarriak inferitzeko. Are gehiago, bere erroreak detektatu ditzake, terminaleko mezuak chat-era kopiatu/itsatsi behar izan gabe.

## Adibide bat nahi? Hemen duzu!

Post honen lehen zirriborroa Copilot bidez sortua izan da. Besterik gabe, *"Sortu post berri bat, euskeraz, Copilot Agent Mode-ri buruz (...)"* esan diot eta berak sortu du fitxategia eta txertatu du testua.

Hala esaten badiogu, berak bakarrik instalatuko digu *Hugo* gure ordenagailuan eta webgune estatikoa sortuko du, horretarako komandoak exekutatuz. 

Bidean hanka sartu edo arazorik aurkituko balu, terminaleko mezuak irakurri eta berak bakarrik konpontuko ditu. 

## Hausnarketak

- Horrelako garapen tresnak, garapen prozesuaren demokratizatzea ekarriko du.
- Hezkuntza arloan, *powerpoint*, txosten, bideo eta bestelako edukiez gain, **irakasle askok haien aplikazio edo tresna propioak sortzeko gaitasuna izango dute**.
- Nahiz eta Copilot kode itxia izan, eta atzetik ChatGPT edota Claude ereduak erailtzen dituen (komertzialak hauek ere), **kode irekiko alternatibak ez daude urrun**. Momentuz, kodea automatikoki konpletazeko eta edizioak egiteko alternatiba askeak jadanik badaude ([llama.vscode](https://github.com/ggml-org/llama.vscode), [TabNine](https://github.com/codota/TabNine), [Void](https://voideditor.com/), [TabbyML](https://github.com/TabbyML/tabby?tab=readme-ov-file)) eta agente moduko tresnak baita ere ([OpenHands](https://github.com/All-Hands-AI/OpenHands?tab=readme-ov-file))irakasle askok haien aplikazio edo tresna propioak sortzeko gaitasuna izango dute