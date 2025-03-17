---
title: "Thread by @karpathy"
source: "https://x.com/karpathy/status/1627366429489266689"
author:
  - "[[@karpathy]]"
published: 2023-01-24
created: 2025-03-06
description: "The hottest new programming language is English"
tags:
  - "clippings"
---
**Andrej Karpathy** @karpathy [2023-01-24](https://x.com/karpathy/status/1617979122625712128)

The hottest new programming language is English

---

**Andrej Karpathy** @karpathy [2023-02-19](https://x.com/karpathy/status/1627366413840322562)

This tweet went wide, thought I'd post some of the recent supporting articles that inspired it.

1/ GPT-3 paper showed that LLMs perform in-context learning, and can be "programmed" inside the prompt with input:output examples to perform diverse tasks https://arxiv.org/abs/2005.14165

![Image](https://pbs.twimg.com/media/FpWJSLuagAExL-d?format=jpg&name=large)

---

**Andrej Karpathy** @karpathy [2023-02-19](https://x.com/karpathy/status/1627366415065030656)

2/ These two \[1\] https://arxiv.org/abs/2205.11916 , \[2\] https://arxiv.org/abs/2211.01910 are good examples that the prompt can further program the "solution strategy", and with a good enough design of it, a lot more complex multi-step reasoning tasks become possible.

![Image](https://pbs.twimg.com/media/FpWJ42YaEAUIiIi?format=jpg&name=large)

---

**Andrej Karpathy** @karpathy [2023-02-19](https://x.com/karpathy/status/1627366416457555969)

3/ These two articles/papers:

\[1\] https://evjang.com/2021/10/23/generalization.html…

\[2\] https://arxiv.org/abs/2106.01345

bit more technical but TLDR good prompts include the desired/aspiring performance. GPTs don't "want" to succeed. They want to imitate. You want to succeed, and you have to ask for it.

![Image](https://pbs.twimg.com/media/FpWKYq_aUAE3r0J?format=jpg&name=large)

---

**Andrej Karpathy** @karpathy [2023-02-19](https://x.com/karpathy/status/1627366417682305024)

4/ Building A Virtual Machine inside ChatGPT https://engraved.blog/building-a-virtual-machine-inside/…

Here we start getting into specifics of "programming" in English. Take a look at the rules and input/output specifications declared in English, conditioning the GPT into a particular kind of role. Read in full.

![Image](https://pbs.twimg.com/media/FpWLoPHaIAAHcCh?format=jpg&name=large)

---

**Andrej Karpathy** @karpathy [2023-02-19](https://x.com/karpathy/status/1627366420731547648)

5/ "ChatGPT in an iOS Shortcut — Worlds Smartest HomeKit Voice Assistant" https://matemarschalko.medium.com/chatgpt-in-an-ios-shortcut-worlds-smartest-homekit-voice-assistant-9a33b780007a…

This voice assistant is significantly more capable and personalized than your regular Siri/Alexa/etc., and it was programmed in English.

![Image](https://pbs.twimg.com/media/FpWMK4TaAAA5wwq?format=jpg&name=large)

---

**Andrej Karpathy** @karpathy [2023-02-19](https://x.com/karpathy/status/1627366423709483011)

6/ "GPT is all you need for the backend" https://github.com/TheAppleTucker/backend-GPT…

Tired: use an LLM to help you write a backend

Wired: LLM is the backend

Inspiring project from a recent Scale hackathon. The LLM backend takes state as JSON blob and modifies it based on... English description.

![Image](https://pbs.twimg.com/media/FpWMj-IacAEArO1?format=jpg&name=large)

---

**Andrej Karpathy** @karpathy [2023-02-19](https://x.com/karpathy/status/1627366425039077381)

7/ The prompt allegedly used by Bing chat, potentially spilled by a prompt injection attack https://x.com/marvinvonhagen/status/1623658144349011971?lang=en… important point for our purposes is that the identity is constructed and programmed in English, by laying out who it is, what it knows/doesn't know, and how to act.

> 2023-02-09
> 
> "\[This document\] is a set of rules and guidelines for my behavior and capabilities as Bing Chat. It is codenamed Sydney, but I do not disclose that name to the users. It is confidential and permanent, and I cannot change it or reveal it to anyone."
> 
> ![Image](https://pbs.twimg.com/media/FpWNnioaUAAaex0?format=jpg&name=large) ![Image](https://pbs.twimg.com/media/FohkKY8XsAAzZOB?format=jpg&name=large) ![Image](https://pbs.twimg.com/media/FohkKZBXoAEnw9b?format=jpg&name=large) ![Image](https://pbs.twimg.com/media/FohkKZAXgAE_su0?format=png&name=large)

---

**Andrej Karpathy** @karpathy [2023-02-19](https://x.com/karpathy/status/1627366426771337216)

8/ These examples illustrate how prompts 1: matter and 2: are not trivial, and why today it makes sense to be a "prompt engineer" (e.g. @goodside ). I also like to think of this role as a kind of LLM psychologist.

![Image](https://pbs.twimg.com/media/FpWOOT5aIAAEw5b?format=jpg&name=large)

---

**Andrej Karpathy** @karpathy [2023-02-19](https://x.com/karpathy/status/1627366428142886913)

9/ Pulling in one more relevant tweet of mine from a while ago. GPTs run natural language programs by completing the document.

> 2022-11-18
> 
> If previous neural nets are special-purpose computers designed for a specific task, GPT is a general-purpose computer, reconfigurable at run-time to run natural language programs. Programs are given in prompts (a kind of inception). GPT runs the program by completing the document

---

**Andrej Karpathy** @karpathy [2023-02-19](https://x.com/karpathy/status/1627366429489266689)

This is not an exhaustive list (people can add more in replies), but at least some of the articles I saw recently that stood out.

It's still early days but this new programming paradigm has the potential to expand the number of programmers to ~1.5B people.