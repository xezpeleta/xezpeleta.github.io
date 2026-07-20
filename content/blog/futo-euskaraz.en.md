---
title: "Basque predictive text on mobile, respecting privacy"
date: 2026-07-20
draft: false
tags: ["ai", "euskara", "basque", "autocompletion", "gboard", "transformer", "llama", "latxa", "futo", "auto-osaketa"]
---


## TL;DR

I've trained a small language model to bring Basque predictive text to Android. It can be used with [**FUTO Keyboard**](https://keyboard.futo.tech/) on a phone. Much like Google's well-known *Gboard*, it can predict the next word and correct mistakes.

## About auto-completion

Auto-completion and similar writing-assist technologies aren't new. They've been with us for a long time. In recent years, however, driven by artificial intelligence, great strides have been made. These are the main options available to us today:

- **Dictionary-based word completion**: the most classic and basic form of auto-completion. When the user types "ira", it looks up words in the dictionary that start the same way and suggests "iragana" or "irabazi". In addition, the most frequently used words can be prioritized.
- **Automatic correction**: basic (dictionary-based) or advanced; capable of detecting and correcting mistakes by understanding the full context.
- **Context completion**: The ability to guess the next word (or words) using the entire written message (or a large part of it). In the best case, it can even guess without you having started writing a new sentence!
## Here too, Google dominates

Google was a pioneer in incorporating these technologies into its *Gboard* keyboard across many languages. But how on earth is it able to guess the word you have in mind?

The secret lies in a small language model stored and run on the phone itself. This small model, based on the *LSTM* architecture, is trained via [*Federated Learning*](https://en.wikipedia.org/wiki/Federated_learning), with the help of millions of users.

> *Gboard*  Do you use it? Did you know your phone wakes up in the middle of the night and shares the new words it has learned with millions of other phones?

It's a remarkable invention. And, according to them, they do all of this [respecting privacy](https://arxiv.org/abs/2305.18465). But how can we know for sure that this is the case? Without having the code at hand and no chance to inspect it, can we be certain that Google does what it claims?

## FUTO keyboard, the "open" alternative

One of the best-known alternatives for Android phones is the [**FUTO Keyboard**](https://keyboard.futo.tech/), with privacy as one of its main features.

Beyond the usual dictionary-based word completion, it [offers the option to use a small model based on the *Transformers* architecture](https://docs.keyboard.futo.tech/settings/textprediction), for auto-completion and also for correction. Unfortunately, the project **only offers an English model**. But if we want, we can choose any other model easily.

## And what if we build a Basque *Transformers* model?

So, if we want an advanced ability to predict the next word in Basque, we need our own *Transformer* model. I've been learning and running experiments on these topics over the last few days (more on this soon). And putting what I've learned into practice... surprise! it seems to be working!

You'll find all the details on the [FUTO-Basque project website](https://github.com/itzune/futo-basque). I used a (portion of the) [Latxa Corpus v2](https://huggingface.co/datasets/HiTZ/latxa-corpus-v2) dataset for training.

When you add this model, it will offer us Basque next-word suggestions, based on the text we've written beforehand.

![Next-word predictions in the FUTO keyboard, while typing in Basque.](/images/futo-next-word.gif)

And it also helps us correct mistakes automatically:

![Automatic mistake correction in Basque with the FUTO keyboard.](/images/futo-correction.gif)

## How to install FUTO with Basque predictions?

1. [Install *FUTO Keyboard*](https://keyboard.futo.tech/#download), however you prefer (*Play Store* or *F-Droid*).
2. Add a keyboard configuration and at least one language:
	 - Type: *QWERTY +1* 
	 - Language: Basque (Euskara)
	 - Dictionary: choose the [Basque dictionary](https://keyboard.futo.tech/dictionaries?locale=eu-ES)
3. Download [the model from the Futo-Basque project's *Release* section](https://github.com/itzune/futo-basque/releases/download/v2.0.0/eu_futo_v2.gguf) to your phone (it's a *.gguf* file, about 48MB)
4. Import the Basque model:
	 - *Settings* > *Languages & Models* > *Import model* (select the gguf file downloaded in the previous step)

## And when we mix more than one language?

It's a common concern for multilingual speakers. We're always mixing different languages, even within the same conversation.

For such cases, FUTO offers [a specific setting](https://docs.keyboard.futo.tech/settings/languagesmodels#enable-multilingual-typing). Add the languages you want to use, each with its own dictionary and settings, and enable the "*Multilingual typing*" option for all the languages you want to mix.

!["Multilingual typing" option enabled, to mix different languages.](/images/futo-multilingual.jpg)

Thanks to this, without having to switch languages back and forth, features like text completion and correction will be available across different languages.

## Basque on par with the major languages

There's [a thread on FUTO's GitHub](https://github.com/futo-org/android-keyboard/issues/1212) discussing this topic: many people want the ability to complete the next word in their own language. French, Greek, Norwegian, Swedish, or even Turkish are being requested and awaited. For now, besides the official English model, as far as I know only a few are available: Portuguese and Polish. And now, Basque!


> FUTO uses its own *"FUTO Source First License"*. It makes the code available and modifiable, but with some limitations. Among others, commercial use is not permitted.
>
>Because of this, according to organizations such as OSI (Open Source Initiative) or FSF (Free Software Foundation), **FUTO does not meet the requirements to be classified as free/open-source software**.
