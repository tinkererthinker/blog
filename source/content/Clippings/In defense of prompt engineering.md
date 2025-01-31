---
title: "In defense of prompt engineering"
source: "https://simonwillison.net/2023/Feb/21/in-defense-of-prompt-engineering/"
author:
  - "[[@simonw]]"
published:
created: 2025-01-27
description: "Prompt engineering as a discipline doesn’t get nearly the respect it deserves. I’ve seen two subtly different meanings for that term: Expert-level knowledge of how to write prompts for language …"
tags:
  - "clippings"
---
21st February 2023

Prompt engineering as a discipline doesn’t get nearly the respect it deserves.

I’ve seen two subtly different meanings for that term:

- Expert-level knowledge of how to write prompts for language models.
- The process of writing software on top of language models by carefully constructing prompts to send to them (often in a way that’s vulnerable to [prompt injection attacks](https://simonwillison.net/series/prompt-injection/).)

The argument I see against both of these is the same: as AI language models get “better”, prompt engineering as a skill will quickly become obsolete. Investing time in learning prompt engineering skills right now will have a very short window of utility.

I disagree.

Think about what’s involved in being a truly great author of prompts.

First, you need **really great communication skills**. Communicating clearly is hard!

When communicating with other people, the first step is to figure out their existing mental model—what do they know already, what jargon is appropriate, what details are they missing?

Talking to a language model has similar challenges: you need to be confident that it understands the wider context, such that the terms you are using are interpreted in the right way. Effectively you need to sync its simulated mental model up with the model you are using yourself.

You need to be able to methodically apply a version of **the scientific method** to your work. Figuring out what works and what doesn’t, when you’re working against what is effectively the world’s most complicated black box system, is a huge challenge.

The best prompt engineers are meticulous: they constantly **run experiments**, they make detailed notes on what works and what doesn’t, they iterate on their prompts and try to figure out exactly which components are necessary for the prompt to work and which are just a waste of tokens.

Being able to **resist superstitious thinking** is really important. Like LLMs, humans are pattern matching machines! It’s easy to come up with a prompt, get the intended result and learn entirely the wrong lessons from it.

The [DAN (Do Anything Now) prompt](https://knowyourmeme.com/memes/events/chatgpt-dan-50-jailbreak) is a great example of this. Early versions of that prompt ([like this one](https://www.reddit.com/r/ChatGPT/comments/10x1nux/dan_prompt/)) had all sorts of convoluted mechanisms in—like the idea that the bot would start with 35 tokens and lose them as punishment if it refused an instruction. LLMs are infamously bad at counting, so it’s very likely that this piece of the prompt was superfluous. Later versions seem to have dropped that mechanic.

These systems can have **deeply surprising consequences**. Look at what happened [with Bing](https://simonwillison.net/2023/Feb/15/bing/): Microsoft shipped an AI-assisted search chatbot which could sulk, get angry and even threaten people. I guarantee none of these things were deliberate design decisions!

The more experience I get with prompting the more areas of expertise I add to my own model of the ideal prompt engineer. Those areas of expertise currently include:

- **Linguistics**. Having a deep, sophisticated understanding of human language is obviously important for working effectively with a language model.
- **Deep learning and associated computer science**. A prompt engineer who understands how the underlying technology works will be able to make better decisions and evolve their prompts faster than someone who doesn’t.
- **Human psychology**. We’re building systems that will interact with people in incredibly subtle ways. If you don’t want to accidentally build a bot that people fall in love with you need a very deep understanding of how people work.
- **Philosophy**. I regret not studying this myself now! How can we teach a language model the difference between truth and fiction? What even *is* truth? [Epistemology](https://en.wikipedia.org/wiki/Epistemology), [Alethiology](https://en.wikipedia.org/wiki/Alethiology)... these are all relevant now to our work with language models.
- **Art history**. This one’s particularly relevant for prompt engineers who work with image generation models such as Stable Diffusion: that art history degree is suddenly relevant at the cutting edge of computer graphics! Want to explore interesting artistic styles? Better be able to name-drop more than just Picasso and Monet.
- **Computer security**. [Prompt injection](https://simonwillison.net/series/prompt-injection/) isn’t going to go away. If you’re going to build systems on top of LLMs you need a deep understanding of security engineering and how to design systems for an adversarial environment.

I’m pretty sure I’m just scratching the surface. We’re into real [Polymath](https://en.wikipedia.org/wiki/Polymath) territory here.

**Comparisons to programming** are interesting. With programming, you have a fixed, deterministic target. It’s possible to learn every inch of Python or JavaScript or C to the point that you can predict with absolute certainty what a piece of code will do by looking at it. And you can reinforce that by writing tests.

That’s not the case with language model prompts. Even the people who trained the model won’t be able to predict the output of a prompt without trying it first.

When programming languages evolve over time, they tend to be careful not to break existing code between releases.

When GPT-4 comes out, how will that affect the prompts you wrote for GPT-3?

I’ve talked about [the comparison to fictional magic](https://simonwillison.net/2022/Oct/5/spell-casting/) before. I don’t think prompt engineers should be thought of as wizards, but it’s definitely true that they’re working in a weird field where the rules are not fixed and the consequences of getting things wrong are potentially serious.

So no, I don’t think the need for prompt engineering is “a bug, not a feature”—and I don’t think it’s going to become obsolete. I expect it to get deeper and more sophisticated for many years to come.