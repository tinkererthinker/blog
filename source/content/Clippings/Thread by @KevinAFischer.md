---
title: "Thread by @KevinAFischer"
source: "https://x.com/KevinAFischer/status/1662853371118641154"
author:
  - "[[@KevinAFischer]]"
published: 2023-05-28
created: 2025-02-18
description: "I don't talk much about this - I obtained one of the first FDA approvals in ML + radiology and it informs much of how I think about AI syste"
tags:
  - "clippings"
---
I don't talk much about this - I obtained one of the first FDA approvals in ML + radiology and it informs much of how I think about AI systems and their impact on the world. If you're a pure technologist, you should read the following: 

There's so much to unpack for both why Geoff was wrong, and why his future predictions should not be taken seriously either. 

Geoff made a classic error that technologists often make, which is to observe a particular behavior (identifying some subset of radiology scans correctly) against some task (identifying hemorrhage on CT head scans correctly), and then to extrapolate based on that task alone. 

The reality is that reducing any job, especially a wildly complex job that requires a decade of training, to a handful of tasks is quite absurd. 

Here's a bunch of stuff you wouldn't know about radiologists unless you built an AI company WITH them instead of opining about their job disappearing from an ivory tower. 

(1) Radiologists are NOT performing 2d pattern recognition - they have a 3d world model of the brain and its physical dynamics in their head. The motion and behavior of their brain to various traumas informs their prediction of hemorrhage determination. 

(2) Radiologists have a whole host of grounded models to make determinations, and actually, one of the most important first order determination they make is whether there is anything notably wrong with a brain structure that "feels" off. As a result, classifiers aren’t actually performing the same task even as radiologists. 

(3) Radiologists, because they have a grounded brain model, only need to see a single example of a rare and obscure condition to both remember it and identify it in the future. This long tail of rare conditions to avoid missing is a large part of their training, and no one has any clue how to make a model that acts similar in this way. 

(4) There’s so many ways to make Radiologist lives easier instead of just replacing them, it doesn’t even make sense to try. I interviewed and hired 25 radiologists, whose primary and chief complaint was that they had to reboot their computers several times a day. 

(5) A large part of the radiologist job is communicating their findings with physicians, so if you are thinking about automating them away you also need to understand the complex interactions between them and different clinics, which often are unique. 

(6) Every hospital is a snowflake, data is held under lock and key, so your algorithm might not work in a bunch of hospitals. Worse, the imagenet datasets have such wildly different feature sets they don’t do much for pretraining for you. 

(7) Have you ever tried to make anything in healthcare? The entire system is optimized to avoid introducing any harm to patients - explaining the ramifications of that would take an entire book, but suffice to say even if you had an algorithm that could automate away radiologists I don’t even know if you could create a viable adoption strategy in the US regulatory environment. 

(8) The reality is that for every application, the amount of specific and UNKNOWABLE domain knowledge is immense. 

LONG STORY SHORT: thinkers have a pattern where they are so divorced from implementation details that applications seem trivial, when in reality, ==the small details are exactly where value accrues. ==

Should you be worried about GPT5 being used to automate vulnerability detection on websites before they’re patched? Maybe. Should you be worried GPT5 is going to interact with SOCIAL systems and destroy our society single-handedly? No absolutely not.