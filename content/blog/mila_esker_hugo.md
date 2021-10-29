---
title: "Mila esker Hugo"
date: 2021-10-27T21:55:58+02:00
draft: true
categories:
- Web development
tags:
- hugo
- web
- static
---

Blog berri hau sortzen [Hugo](https://gohugo.io)k lagundu dit. Hauek dira bere abantaila nagusiak:

- Azkartasuna: 1ms baina gutxiago orri bat kargatzeko
- Malgutasuna: menu eta eduki mota ezberdinak, taxonomiak, etab.
- Formatu askorekin bateragarria: Markdown, HTML, AsciiDoc, RST, etab.
- _Go Template_ delakoetan oinarrituta: datuak modu anitzetan azaltzeko gaitasuna ematen du
- Eduki eleanitza sortzeko gaitasuna


Besteak beste, webguneak, blogak edota dokumentazio proiektuak argitaratzeko erabili dezakegu *Hugo*.

<!--more-->


## Hugo instalazioa

Hugo instalatzeko aukera ezberdinak ditugu. Debian edo Ubuntu bada zure sistema, [Hugoren GitHub errepositoriotik](https://github.com/gohugoio/hugo/releases) DEB paketea deskargatzea eta instalatzea gomendatzen dizut.


## Sortu Hugo webgunea

Jadanik instalatuta? Sor dezagun gure lehen Hugo webgunea agindu bakar batekin:

```
hugo new site new-site
```

## Sortu webguneko lehen edukia

Edukia formatu ezberdinetan ulertzen du. Adibidez, Markdown lengoian idatzi nahi badugu `.md` extentsioa gehituko diogu edukiari:

```
hugo new blog/kaixo-mundua.md
```

Honek `content/blog` direktorioan fitxategi berri bat sortuko digu. Sortutako fitxategiari bistazo bat botatzen badiogu ikusiko dugu buruko batzuk gehitu dizkiola.

Hor ikus dezakegu momentuz artikulu hau _Draft_ edo zirriborro moduan dagoela. Testua idatzi eta zuzentzeaz bukatzen dugunean, `draft: false` jarriko beharko dugu.

## Hugo Theme berri bat sortu

Webgunearen itxura Tailwind erabiliz pertsonalizatu nahi dudanez, [hugo-theme-tailwindcss-starter](https://github.com/dirkolbrich/hugo-theme-tailwindcss-starter) erabili dut.

```
cd themes
git clone https://github.com/dirkolbrich/hugo-theme-tailwindcss-starter new-theme-name
```

Ezabatu git direktorioa eta Iinstalatu beharrezko node paketeak:

```
cd new-theme-name
rm -fr .git
npm install
```

Orain, aldatu `config.toml` konfigurazio fitxategia _theme_ berria erabiltzeko.

```
# config.toml
theme = "new-theme-name"
```

Azkenik, jar dezagun martxan zerbitzaria:

```
cd new-site
hugo server -D --disableFastRender
```

## Gure Theme berria aldatzen

Gehitu berri dugun _theme_ hau ez dago erabiltzeko moduan. Lan dexente egin beharko dugu itxura aldatzeko.

new-site/themes/new-theme-name/layout

Garapenean, Helper hauek azalduko dira:
/partials/dev-parameters.html
/partials/dev-size-indicator.html