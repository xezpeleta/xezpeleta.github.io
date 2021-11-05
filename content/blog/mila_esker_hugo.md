---
title: "Mila esker, Hugo"
date: 2021-11-05T20:05:58+02:00
draft: false
categories:
- Web
tags:
- hugo
- web
- markdown
- github
- vscode
ShowToc: true
---

Blog berria sortzen [Hugo](https://gohugo.io)k lagundu dit. [**Webgune estatikoak**](https://www.cloudflare.com/learning/performance/static-site-generator/) sortzeko tresna bikaina da; [Jekyll](https://jekyllrb.com/), [Gatsby](https://www.gatsbyjs.com/) edo [Ghost](https://ghost.org/) bezalako zeozer dela esan daiteke.

Hauek dira bere abantaila nagusiak:

- Azkartasuna
- Malgutasuna
- Erreztasuna
- Iturri formatu askorekin bateragarria (Markdown, HTML, AsciiDoc, RST, etab.)
- Eduki eleanitzak sortzeko gaitasuna

Besteak beste, webguneak, blogak edota dokumentazio proiektuak argitaratzeko erabili dezakegu *Hugo*.

![Hugoren webgunea](/images/2021-11-02-21-20-04.png) 

## Instalazioa

Hugo instalatzeko aukera ezberdinak ditugu. Debian edo Ubuntu bada zure sistema, [Hugoren errepositoriotik](https://github.com/gohugoio/hugo/releases) **DEB paketea** deskargatzea eta instalatzea gomendatzen dizut.

## Lehen urratsak

### Sortu webgune bat

Jadanik instalatuta? Sor dezagun gure lehen Hugo webgunea:

```console
$ hugo new site nirewebgunea
```

### _Theme_ bat aukeratu

Ezer baino lehen, gure webguneak zein itxura izango duen erabaki beharko dugu. Hasteko [Ananke](https://themes.gohugo.io/gohugo-theme-ananke/) _theme_ edo gaia instalatu dezakegu:

```console
$ cd nirewebgunea/
$ git init
$ git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke
```

Eta konfigurazioan ezarri:

```console
$ echo theme = \"ananke\" >> config.toml
```

> _Oharra_: TOML lengoaia ez baduzu gustoko, YAML erabili dezakezu (`config.yaml`) 

Aukeratzeko _theme_ pila bat ditugu [themes.gohugo.io](ttps://themes.gohugo.io/) webgunean. Nire kasuan [PaperMod](https://themes.gohugo.io/themes/hugo-papermod/) delakoa aukeratu dut (momentuz).

### Edukia sortzen

Edukia formatu ezberdinetan ulertzeko gai da. Adibidez, [Markdown](https://guides.github.com/features/mastering-markdown/) lengoian idatzi nahi badugu `.md` extentsioa gehituko diogu edukiari:

```console
$ hugo new blog/kaixo-mundua.md
```

Honek `content/blog` direktorioan fitxategi berri bat sortuko digu:

`Fitxategia: content/blog/kaixo-mundua.md`
```markdown
---
title: "Kaixo Mundua"
date: 2021-11-02T20:05:58+02:00
draft: true
---
```

Hor ikus dezakegu momentuz artikulu hau _Draft_ edo zirriborro moduan dagoela. Testua argitaratu nahi dugunean, `draft: false` jarri beharko dugu.

## Hasieratu Hugo zerbitzaria

Gure ordenagailuan webgunearen aurrebista ikusteko:

```console
$ hugo server -D
```
> _Oharra_: `-D` parametroak zirriborroak ikusteko aukera aktibatuko du.

Sartu [localhost:1313](http://localhost:1313) helbidera. Aldaketak egin ahala emaitza nabigatzailean ikusiko dugu.

## Webgunea argitaratu

Web estatikoen abantaila nagusia argitaratzeko erreztasuna da. Dohainezko zerbitzu asko daude webgune estatikoak argitaratzeko aukera ematen dutenak, besteak beste: [Netlify](https://docs.netlify.com/configure-builds/common-configurations/hugo/), [CloudFlare](https://developers.cloudflare.com/pages/framework-guides/deploy-a-hugo-site#deploying-with-cloudflare-pages), [Gitlab](https://gohugo.io/hosting-and-deployment/hosting-on-gitlab/) edota [**Github**](https://gohugo.io/hosting-and-deployment/hosting-on-github/). Nik azken hau aukeratu dut, gehien ezagutzen dudan ingurunea baita.

### Github Action

Horretarako **Github Action** bat sortu behar izan dut nire errepositorioan:


`Fitxategia: .github/workflows/gh-pages.yml`
```yml
name: github pages

on:
  push:
    branches:
      - main  # Set a branch to deploy
  pull_request:

jobs:
  deploy:
    runs-on: ubuntu-20.04
    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true  # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'
          extended: true

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        if: github.ref == 'refs/heads/main'
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public

```

Aldaketak aplikatu eta igo ondoren, definitu berri dugun Github Action hori exekutatuko da. Honek `gh-pages` delako _branch_ bat sortuko du webgunearekin.

{{< figure src="/images/2021-11-03-08-59-25.png" align=center alt="gh-pages branch berria" width="300px" >}}

### GitHub Pages

Hain zuzen ere, hau da aukeratu beharko dugun adarra, _Settings_ - _**Pages**_ atalean:

![Settings Pages atala](/images/2021-11-03-09-05-14.png)

Eta listo! Honekin gure edukia moldatzen dugun aldiro webgunea automatikoki eguneratuko da.


## Tresna erabilgarriak

Nire kasuan web edukia _Markdown_ testu fitxategien bidez idaztea erabaki dut. Horretarako VSCode erabiltzen dudanez, badaude benetan erabilgarriak diren hainbat extentsio:

- ["Paste Image" extentsioa](https://marketplace.visualstudio.com/items?itemName=mushan.vscode-paste-image):
Irudiak copy-paste bidez gehitzen lagunduko digu. Ezarri dudan konfigurazioa (_Workspace_ eremuan):


`Fitxategia: .vscode/settings.json`
```json
{
    "pasteImage.basePath": "${projectRoot}/static",
    "pasteImage.path": "${projectRoot}/static/images",
    "pasteImage.prefix": "/"
}
```

- ["Hugofy" extentsioa](https://marketplace.visualstudio.com/items?itemName=akmittal.hugofy):
VSCode ingurunetik atera gabe ia dena egin nahi badugu (postak sortu, zerbitzaria gelditu eta hasi etab...)
- [Beste extentsio interesgarri batzuk](https://gohugo.io/tools/editors/#visual-studio-code): egia esan, hauek ez ditut probatu ere egin

