---
title: "GitHub Copilot Agent Mode: An Intelligent Development Partner"
date: 2024-02-12
draft: false
tags: ["github", "ai", "vscode"]
cover:
    image: "/images/copilot-agent-mode.png"
    alt: "GitHub Copilot Agent Mode"
    caption: "The agent awakens"
---

GitHub Copilot has introduced a significant advancement: [Agent Mode](https://github.blog/news-insights/product-news/github-copilot-the-agent-awakens/). With this new feature, using the VS Code editor's text interface, it can autonomously analyze, modify, and execute files in your project.

## What is Agent Mode or SWE agent?

Agent Mode expands GitHub Copilot's capabilities, transforming it from a simple code completer to an autonomous development assistant. The artificial intelligence can analyze, understand, and modify project files, as well as execute terminal commands.

## How does it work?

Agent Mode has special capabilities to improve its code and fix errors. It can repeatedly refine its proposals, identify and automatically fix errors. It can suggest and execute terminal commands, and analyze and fix runtime errors.

> *And it will continue working until your requested task is complete. Instead of just performing the specified task, it can now infer complementary tasks that weren't specified but are necessary. Moreover, it can detect its own errors without needing to copy/paste terminal messages to the chat.*

In agent mode, Copilot doesn't just limit itself to improving its output; it also analyzes the results of that output. And it will continue working until your requested task is complete. Instead of just performing the specified task, it can now infer complementary tasks that weren't specified but are necessary. Moreover, it can detect its own errors without needing to copy/paste terminal messages to the chat.

## Want an example? Here you have it!

The first draft of this post was created through Copilot. Simply by saying *"Create a new post, in Basque, about Copilot Agent Mode (...)"*, it created the file and inserted the text.

If we tell it to, it will automatically install *Hugo* on our computer and create the static website by executing the necessary commands.

If it makes a mistake or encounters any problems along the way, it will read the terminal messages and fix them on its own.

## Reflections

- Such development tools will lead to the democratization of the development process.
- In education, beyond PowerPoint presentations, reports, videos, and other content, **many teachers will have the ability to create their own applications or tools**. It will be similar in other sectors as well.
- It's already clear that it can understand and write **well in Basque**, at least when using `Claude 3.5 Sonnet` as the model.
- Although Copilot is closed source and uses commercial models like ChatGPT, Gemini, or Claude behind the scenes, **open-source alternatives are not far behind**. Currently, there are already free alternatives for automatic code completion and editing ([llama.vscode](https://github.com/ggml-org/llama.vscode), [TabNine](https://github.com/codota/TabNine), [Void](https://voideditor.com/), [TabbyML](https://github.com/TabbyML/tabby?tab=readme-ov-file)) and agent-like tools as well ([OpenHands](https://github.com/All-Hands-AI/OpenHands?tab=readme-ov-file))