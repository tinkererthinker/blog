---
title: "A Barebones Guide to Mechanistic Interpretability Prerequisites — Neel Nanda"
source: "https://www.neelnanda.io/mechanistic-interpretability/prereqs"
author:
  - "[[Neel Nanda]]"
published: 2022-10-24
created: 2025-01-27
description: "Co-authored by Neel Nanda and Jess Smith    Check out    Concrete Steps for Getting Started in Mechanistic Interpretability    for a better starting point   Why does this exist?  People often get intimidated when trying to get into AI or AI Alignment research. People often think that the gulf betwee"
tags:
  - "clippings"
---
*Co-authored by Neel Nanda and Jess Smith*

**Check out** [**Concrete Steps for Getting Started in Mechanistic Interpretability**](https://neelnanda.io/getting-started) **for a better starting point**

## Why does this exist?

People often get intimidated when trying to get into AI or AI Alignment research. People often think that the gulf between where they are and where they need to be is huge. This presents practical concerns for people trying to change fields: we all have limited time and energy. And for the most part, people wildly overestimate the actual core skills required.

This guide is our take on the essential skills required to understand, write code and ideally contribute useful research to mechanistic interpretability. We hope that it’s useful and unintimidating. :) 

## Core Skills:

- ### Maths

	- Linear Algebra: [3Blue1Brown](https://www.youtube.com/watch?v=fNk_zzaMoSs) or [Linear Algebra Done Right](https://linear.axler.net/)
	- Core goals - to deeply & intuitively understand these concepts:
		- Basis
		- Change of basis
		- That a vector space is a geometric object that doesn’t necessarily have a canonical basis
		- That a matrix is a linear map between two vector spaces (or from a vector space to itself)
		- Bonus things that it’s useful to understand: 
			- What’s singular value decomposition? Why is it useful?
			- What are orthogonal/orthonormal matrices, and how is changing to an orthonormal basis importantly different from just any change of basis?
			- What are eigenvalues and eigenvectors, and what do these tell you about a linear map?
	- Probability basics
		- Basics of distributions: expected value, standard deviation, normal distributions
		- Log likelihood
		- Maximum value estimators
		- Random variables
		- Central limit theorem
		- Calculus basics
		- Gradients
		- The chain rule
		- The intuition for what backprop is - in particular, grokking the idea that backprop is just the chain rule on multivariate functions

- ### Coding
	- Python Basics
		- The “how to learn coding” market is pretty saturated - there’s a lot of good stuff out there! And not really a clear best one.
		- Zac Hatfield-Dodds recommends Al Sweigart's *Automate the Boring Stuff* and then *Beyond the Basic Stuff* (both readable for free on [inventwithpython.com](https://inventwithpython.com/), or purchasable in books); he's also written some books of exercises. If you prefer a more traditional textbook, [*Think Python 2e*](https://greenteapress.com/wp/think-python-2e/) is excellent and also available freely online.
	- NumPy Basics
		- Try to do the first ~third of these: ​​[https://github.com/rougier/numpy-100](https://github.com/rougier/numpy-100). Bonus points for doing them in pytorch on tensors :)

- ### ML:
	- Rough grounding in ML. 
	- [fast.ai](https://course.fast.ai/) is a good intro, but a fair bit more effort than is necessary. For an 80/20, focus on  Andrej Karpathy’s new video explaining neural nets: [https://www.youtube.com/watch?v=VMj-3S1tku0](https://www.youtube.com/watch?v=VMj-3S1tku0)
	- [PyTorch](https://pytorch.org/tutorials/) basics
	- Don’t go overboard here. You’ll pick up what you need over time - learning to google things when you get confused or stuck is most of the *real* skill in programming.
	- One goal: build linear regression that runs in Google Colab on a GPU.
	- The main way you will shoot yourself in the foot with PyTorch is when manipulating tensors, and especially multiplying them. **I highly, highly recommend learning how to use** [**einops**](https://einops.rocks/1-einops-basics/) (a library to nicely do any reasonable manipulation of a single tensor) and [einsum](https://rockt.github.io/2018/04/30/einsum) (a built in torch function implementing Einstein Summation notation, to do arbitrary tensor multiplication)
	- If you try doing these things without einops and einsum you will hurt yourself. Do not recommend!
	- Transformers - probably the biggest way mechanistic interpretability differs from normal ML is that it’s *really* important to deeply understand the architectures of the models you use, all of the moving parts inside of them, and how they fit together. In this case, the main architecture that matters is a transformer! (This is useful in normal ML too, but you can often get away with treating the model as a black box)
		- My [what is a transformer](https://www.neelnanda.io/transformer-tutorial) and [implementing GPT-2 From Scratch](https://www.neelnanda.io/transformer-tutorial-2) video tutorials
		- [My transformer glossary/explainer](https://dynalist.io/d/n2ZWtnoYHrU1s4vnFSAQ519J#z=pndoEIqJ6GPvC1yENQkEfZYR)
		- **A worthwhile exercise is to fill out the** [**template notebook**](https://www.neelnanda.io/transformer-template), accompanying the tutorial (no copying and pasting!) 
		- The notebook comes with tests so you know that your code is working, and by the end of this you'll have a working implementation of GPT-2!
		- If you can do this, I’d say that you basically fully understand the transformer architecture.
		- Alternate framings that may help give different intuitions: 
			- Nelson Elhage’s [Transformers for Software Engineers](https://blog.nelhage.com/post/transformers-for-software-engineers/) (also useful to non software engineers!)
			- Check out [the illustrated transformer](https://jalammar.github.io/illustrated-transformer/) 
	- Note that you can pretty much ignore the stuff on encoder vs decoder transformers - we mostly care about autoregressive decoder-only transformers like GPT-2, which means that each token can only see tokens before it, and they learn to predict the next token
	- Bonus: [Jacob Hilton’s Deep learning for Alignment syllabus](https://github.com/jacobhilton/deep_learning_curriculum) - this is a lot more content than you strictly need, but is well put together and likely a good use of time to go through at least some of!

Once you have the pre-reqs, my [Getting Started in Mechanistic Interpretability](https://neelnanda.io/getting-started) guide goes into how to get further into mechanistic interpretability!

Note that there are a lot more skills in the “nice-to-haves”, but I think that generally the best way to improve at something is by getting your hard dirty and engaging with the research ideas directly, rather than making sure you learn every nice-to-have skill first - if you have the above, I think you should just jump in and start learning about the topic! Especially for the coding related skills, your focus should not be on getting your head around concepts, it should be about *doing*, and actually writing code and playing around with the things - the challenge of making something that actually works, and dealing with all of the unexpected practical problems that arise is the best way of really getting this.