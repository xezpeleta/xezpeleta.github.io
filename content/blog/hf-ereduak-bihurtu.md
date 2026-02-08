---
title: "Ereduak GGUF formatura bihurtu"
date: 2026-02-08
draft: false
tags: ["llm", "llama.cpp", "gguf", "qwen"]
cover:
    image: "/images/hf-ereduak-bihurtu-cover.png"
    alt: "HF ereduak GGUF formatura bihurtu"
    caption: "HF ereduak GGUF formatura bihurtu"
---

Gida honetan HuggingFace webgunean argitaratuak dauden ereduak GGUF formatura bihurtzeko jarraibideak azaltzen dira.

GGUF formatu honek ereduak gure ordenagailuan modu eraginkorrean erabiltzeko aukera eskaintzen du. Horretarako, [Llama.cpp](https://github.com/ggml-org/llama.cpp) edo [Ollama](https://ollama.com/) bezalako tresnak erabili ditzakegu.

## Llama.cpp deskargatu

Gure ordenagailuan bertan GGUF formatura bihurtzeko, [llama.cpp](https://github.com/ggml-org/llama.cpp)
deskargatu beharko dugu lehenik eta behin, bertako bihurketa tresnak erabili ahal izateko.

```
# Klonatu llama.cpp biltegia
git clone https://github.com/ggml-org/llama.cpp.git
```

## Ingurunea prestatu

Ingurunea prestatu eta beharrezko dependentziak instalatzeko, `uv` erabiliko dugu. Ez baduzu instalatu, [instalatu beharko duzu](https://docs.astral.sh/uv/getting-started/installation/).

```sh
# Sortu ingurune birtuala
cd llama.cpp
uv venv

# Arazorik izanez gero, saiatu Python bertsioa zehazten
# uv venv --python 3.11

# Aktibatu ingurunea
source .venv/bin/activate
```

## Instalatu dependentziak

Kasu honetan, ereduak bihurtzeko ez dugu behar *llama.cpp* osoa instalatzea; soilik bihurketa tresnak erabili ahal izateko liburutegiak beharko ditugu:

```sh
uv pip install -r requirements/requirements-convert_hf_to_gguf.txt
```

## Bihurtu GGUF formatura

HuggingFace webgunean dagoen ereduaren identifikatzailea (*<user_id>/<repo_id>*) pasata eta nahi dugun irteera mota zehaztuta,
gure gguf fitxategia sortuko digu:

Kasu honetan, `HiTZ/Latxa-Qwen3-VL-4B-Instruct` ereduaren 4B bertsioa bihurtuko dugu, `f16` eta `q8_0` kuantizazioekin.

```sh
# F16
uv run convert_hf_to_gguf.py HiTZ/Latxa-Qwen3-VL-4B-Instruct --remote --outtype f16

# Q8_0
uv run convert_hf_to_gguf.py HiTZ/Latxa-Qwen3-VL-4B-Instruct --remote --outtype q8_0
```

Agindu hauek gguf fitxategiak sortuko dizkigu (adibidez `HiTZ-Latxa-Qwen3-VL-4B-Instruct-q8_0.gguf`).

## Eredu multimodalentzako (VL) `mmproj` irudi prozesatzailea

VL motako eredu multimodalei (adibidez Latxa VL ereduak) irudiak pasa ahal izateko, irudi kodifikatzailea ere beharko dugu.
`mmproj` izeneko fitxategiak izan ohi dira, ereduaren pisuekin batera elkarbanatu ohi direnak. Jatorrizkoa deskargatu dezakegu eta erabili (kasu honetan, [Qwen ereduarena](https://huggingface.co/Qwen/Qwen3-VL-4B-Instruct-GGUF/blob/main/mmproj-Qwen3VL-4B-Instruct-Q8_0.gguf)).

Hala ere, fitxategi hau ere guk geuk sortu dezkegu, bihurketa scripta bera erabilita eta `--mmproj` parametroa pasata.

```sh
# Sortu mmproj fitxategia `--mmproj` gehituta
uv run convert_hf_to_gguf.py HiTZ/Latxa-Qwen3-VL-2B-Instruct --remote --outfile mmproj-HiTZ-Latxa-Qwen3-VL-2B-Instruct-q8_0.gguf --outtype q8_0 --mmproj
```

## Bestelako kuantizazioak lortzeko

Bestelako kuantizazioak lortu nahi ezkero, Llama.cpp instalazio urratsak jarraitu beharko dituzu eta `llama-quantize` agindua erabili.

```sh
# Kuantizatu Q4_K_M bezala
./llama-quantize ggml-model-f16.gguf ggml-model-Q4_K_M.gguf Q4_K_M
```

Informazio gehiagorako, irakurri [llama-quantize gida](https://github.com/ggml-org/llama.cpp/blob/master/tools/quantize/README.md)


## Erabilera `llama.cpp` bidez

Behin gure gguf fitxategiak sortuta, `llama.cpp` erabiliz ereduak exekutatu ditzakegu gure ordenagailuan bertan.

Honetarako bai, *llama.cpp* [instalatu beharko dugu](https://github.com/ggml-org/llama.cpp/blob/master/docs/install.md).

```sh
# Exekutatu llama-cli gure ereduarekin
llama-cli -m Orai-Kimu-9B-GGUF-Q4_0.gguf
```

Agindu honek terminalean bertan proba azkarrak egiteko aukera emango digu.

Nik nahiago, ordea, OpenAI APIarekin bateragarria den zerbitzaria exekutatu, web interfazea eta guzti!

```sh
llama-server \
    --host localhost \
    --port 8000 \
    --model Gemma-2b-GGUF-Q4_0.gguf 
```

Dena ondo badabil, `http://localhost:8000` helbidean sartu eta hor ikusiko duzu elkarrizketarako web interfaze txukuna martxan.

Ereduak *HuggingFace*-en argitaratuak badaude, zuzenean bertatik exekutatu ditzakegu eskuz deskargatu gabe `-hf` parametroa erabiliz:

```sh
llama-server
    --host localhost \
    --port 8000 \
    -hf unsloth/Qwen3-VL-8B-Instruct-GGUF:UD-Q4_K_XL
```

### Eredu multimodalen inferentzia

Lehen aipatu bezala, eredu multimodalek (VL motakoak) duten berezitasuna irudiak prozesatzeko gaitasuna da. Horretarako, `mmproj` fitxategia zehaztea ezinbestekoa da:


```sh
llama-server --host localhost --port 8000 \
      --model models/Qwen3VL/Qwen3-VL-8B-Instruct-UD-Q4_K_XL.gguf \
      --mmproj models/Qwen3VL/mmproj-F16.gguf \
      --ctx-size 4096 \
      --temp 0.7 \
      --flash-attn on \
      --jinja \
      --n-gpu-layers 99 \
      --top-k 20 \
      --top-p 0.8 \
      --min-p 0.0 \
      --presence-penalty 1.5
```

Gainontzeko parametroen esanahia ezagutzeko, irakurri `llama-server` aginduaren laguntza.

## Erabilera Ollama bidez

Gure GGUF fitxategiak Ollama bidez erabili nahi baditugu, sortu `Modelfile` fitxategi bat ondorengo lerroekin:

```
FROM /path/to/file.gguf
```

Eta ondoren, soilik:

```
ollama create mymodel
```

Informazio gehiagorako, irakurri [Ollama webguneko dokumentazioa](https://docs.ollama.com/import#importing-a-gguf-based-model-or-adapter)


## Igo GGUF fitxategiak gure HF biltegira

Azkenik, fitxategi hauek eskuragarri utzi nahi baditugu, gure HuggingFace biltegira igo ditzakegu `hf` agindua erabiliz.

```
hf upload itzune/Latxa-Qwen3-VL-4B-GGUF HiTZ-Latxa-Qwen3-VL-4B-Instruct-q8_0.gguf
```
