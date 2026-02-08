---
title: "Convert Models to GGUF Format"
date: 2026-02-08
draft: false
tags: ["llm", "llama.cpp", "gguf", "qwen"]
cover:
    image: "/images/hf-ereduak-bihurtu-cover.png"
    alt: "Convert HF models to GGUF format"
    caption: "Convert HF models to GGUF format"
---

This guide explains the steps to convert models published on HuggingFace to GGUF format.

The GGUF format offers the possibility to run models efficiently on our computers. For this, we can use tools like [Llama.cpp](https://github.com/ggml-org/llama.cpp) or [Ollama](https://ollama.com/).

## Download Llama.cpp

To convert to GGUF format locally on our machine, we first need to download [llama.cpp](https://github.com/ggml-org/llama.cpp) to be able to use its conversion tools.

```
# Clone the llama.cpp repository
git clone https://github.com/ggml-org/llama.cpp.git
```

## Prepare the environment

We will use `uv` to prepare the environment and install necessary dependencies. If you haven't installed it, [you will need to install it](https://docs.astral.sh/uv/getting-started/installation/).

```sh
# Create a virtual environment
cd llama.cpp
uv venv

# If you encounter issues, try specifying the Python version
# uv venv --python 3.11

# Activate the environment
source .venv/bin/activate
```

## Install dependencies

In this case, we don't need to install the full *llama.cpp* to convert models; we just need the libraries to use the conversion tools:

```sh
uv pip install -r requirements/requirements-convert_hf_to_gguf.txt
```

## Convert to GGUF format

By passing the identifier of the model located on HuggingFace (*<user_id>/<repo_id>*) and specifying the desired output type, it will create our gguf file:

In this case, we will convert the 4B version of the `HiTZ/Latxa-Qwen3-VL-4B-Instruct` model, with `f16` and `q8_0` quantizations.

```sh
# F16
uv run convert_hf_to_gguf.py HiTZ/Latxa-Qwen3-VL-4B-Instruct --remote --outtype f16

# Q8_0
uv run convert_hf_to_gguf.py HiTZ/Latxa-Qwen3-VL-4B-Instruct --remote --outtype q8_0
```

These commands will create the gguf files (e.g. `HiTZ-Latxa-Qwen3-VL-4B-Instruct-q8_0.gguf`).

## `mmproj` image processor for multimodal models (VL)

To be able to pass images to VL type multimodal models (e.g. Latxa VL models), we will also need the image encoder.
They are usually files named `mmproj`, which are often shared along with the model weights. We can download and use the original one (in this case, [Qwen model's one](https://huggingface.co/Qwen/Qwen3-VL-4B-Instruct-GGUF/blob/main/mmproj-Qwen3VL-4B-Instruct-Q8_0.gguf)).

However, we can also create this file ourselves, using the same conversion script and passing the `--mmproj` parameter.

```sh
# Create mmproj file by adding `--mmproj`
uv run convert_hf_to_gguf.py HiTZ/Latxa-Qwen3-VL-2B-Instruct --remote --outfile mmproj-HiTZ-Latxa-Qwen3-VL-2B-Instruct-q8_0.gguf --outtype q8_0 --mmproj
```

## Obtaining other quantizations

If you want to obtain other quantizations, you will need to follow the Llama.cpp installation steps and use the `llama-quantize` command.

```sh
# Quantize as Q4_K_M
./llama-quantize ggml-model-f16.gguf ggml-model-Q4_K_M.gguf Q4_K_M
```

For more information, read the [llama-quantize guide](https://github.com/ggml-org/llama.cpp/blob/master/tools/quantize/README.md)


## Usage with `llama.cpp`

Once our gguf files are created, we can run the models locally on our computer using `llama.cpp`.

For this, yes, [we will need to install](https://github.com/ggml-org/llama.cpp/blob/master/docs/install.md) *llama.cpp*.

```sh
# Run llama-cli with our model
llama-cli -m Orai-Kimu-9B-GGUF-Q4_0.gguf
```

This command will allow us to do quick tests right in the terminal.

I prefer, however, to run a server compatible with the OpenAI API, complete with a web interface!

```sh
llama-server \
    --host localhost \
    --port 8000 \
    --model Gemma-2b-GGUF-Q4_0.gguf 
```

If everything works well, go to `http://localhost:8000` and there you will see a neat web interface for chatting running.

If existing models are published on *HuggingFace*, we can run them directly from there without manually downloading them using the `-hf` parameter:

```sh
llama-server
    --host localhost \
    --port 8000 \
    -hf unsloth/Qwen3-VL-8B-Instruct-GGUF:UD-Q4_K_XL
```

### Multimodal inference

As mentioned before, the peculiarity of multimodal models (VL type) is the ability to process images. For this, specifying the `mmproj` file is essential:


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

To know the meaning of the rest of the parameters, read the help for the `llama-server` command.

## Usage with Ollama

If we want to use our GGUF files with Ollama, create a `Modelfile` with the following lines:

```
FROM /path/to/file.gguf
```

And then, just:

```
ollama create mymodel
```

For more information, read the [documentation on the Ollama website](https://docs.ollama.com/import#importing-a-gguf-based-model-or-adapter)


## Upload GGUF files to our HF repository

Finally, if we want to make these files available, we can upload them to our HuggingFace repository using the `hf` command.

```
hf upload itzune/Latxa-Qwen3-VL-4B-GGUF HiTZ-Latxa-Qwen3-VL-4B-Instruct-q8_0.gguf
```
