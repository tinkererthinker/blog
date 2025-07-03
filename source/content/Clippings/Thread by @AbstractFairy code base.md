---
title: "Thread by @AbstractFairy"
source: "https://x.com/DefenderOfBasic/status/1782725829635780926"
author:
  - "[[@AbstractFairy]]"
published: 2024-04-23
created: 2025-07-03
description: "The latest stories on X - as told by posts."
tags:
  - "clippings"
---
**Abstract Fairy** @AbstractFairy [2024-04-23](https://x.com/AbstractFairy/status/1782674855189455162)

is there a video/channel about exploring and reviewing open source code?

like, there's a lot to learn from top level gamers commenting on how they play the game, is there smth similar for programming?

---

**Defender** @DefenderOfBasic [2024-04-23](https://x.com/DefenderOfBasic/status/1782725829635780926)

There should be! One trick someone taught me was to start with PRs. A PR cuts through a huge code base by showing the relationship between all the relevant places in the code. I always start by finding the closest PR to the thing I'm looking for

---

**Abstract Fairy** @AbstractFairy [2024-04-23](https://x.com/AbstractFairy/status/1782731718643847673)

whats a PR?

---

**Defender** @DefenderOfBasic [2024-04-23](https://x.com/DefenderOfBasic/status/1782732449858158847)

Sorry, if the open source codebase you're exploring is on GitHub there'll be pull requests (PRs)!

Like when I was trying to find the code in the Godot codebase for touch input I searched "input" in the pull requests tab and glanced through a couple

This acts as essentially a map for me. I can see that this one code file plus this config file is where the actual touch input code is, and how the data flows from user input to handling that input

---

**matthijs** @MatthijsCox [2024-04-23](https://x.com/MatthijsCox/status/1782778234226065645)

Maybe we should find @AbstractFairy a video that shows the whole PR process end-to-end, to show how much non-coding is involved in software development. Issue discussion, GIT, code reviews, testing, documentation, releasing, etc.

---

**Defender** @DefenderOfBasic [2024-04-23](https://x.com/DefenderOfBasic/status/1782778959123361804)

Yeah!! I can't point to a thing that exists already (probably does somewhere) but I kind of want to record it. I think I've gotten much better at this in past years and it would have been super helpful for past me to see it

I think learning to navigate this has allowed me to deliver a ton of value to my team just by asking questions and saving everyone literal weeks of work

> 2024-04-21
> 
> I do this but a lot of people on my team don't (because it's annoying and not fun to dig through old PRs) but it's kind of a super power because I always catch things others don't (only because I go "3 years ago we ran into this edge case. Did you check if it's still relevant?")

---

**matthijs** @MatthijsCox [2024-04-23](https://x.com/MatthijsCox/status/1782781556995621092)

Yeah this is all good stuff. I recall that a colleague once mentioned there exist courses on "the missed semester" that goes into all the stuff that universities often forget to teach regarding coding.