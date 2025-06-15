---
title: "Thread by @betanalpha"
source: "https://x.com/betanalpha/status/1170738390721081347"
author:
  - "[[@betanalpha]]"
published: 2019-09-08
created: 2025-06-15
description:
tags:
  - "clippings"
---
**\\mathfrak{Michael "Shapes Dude" Betancourt}** @betanalpha [2019-09-08](https://x.com/betanalpha/status/1170738390721081347)

There's a subtle ambiguity in the definition of a "derivative of a function" that has a habit of confusing people. The derivative is often introduced as "how quickly a function changes at a point", which would make it a scalar value, at least in one dimension.

But the term "derivative" is also used to denote a function that maps \_each\_ point to the local derivative value around that point.

In other words differentiation can be defined as a map from an entire function and a point to a single number (the derivative at that point) or as a map from an entire function to and entirely new function (the mapping from point to derivative).

Incidentally this is why mathematical notation like $\frac{d(f(x_0))}{dx}$ is sloppy and confusing. You don't differentiate the single value $f(x_0)$ but rather the entire function $f$ and then evaluate it at a point. Hence the much better notation is $\frac{df}{dx}(x_0)$.

One place this confusion arises? In algorithmic differentiation. Automatic differentiation computes the derivative at a point where as symbolic differentiation computes the entire derivative function. Those different outputs are why the implementations are so different.

This "define something as behavior in small neighborhood and then define a function that maps points to local behavior in a small neighborhood around that point" pattern is also all over differential geometry and took me forever to really understand while learning the math.

i.e. the difference between a vector and a vector field, a tensor and a tensor field, a tangent space and a tangent bundle, etc. When first learning you have to be really careful to explicitly lay out what is a point value and what is a function to avoid confusing the two.

This was Sunday morning jet lagged mathematical theater.

---

This is just one example of why any author who doesn’t specify the type of each important definition they introduce is doing you a massive disservice and dumping a load of comprehension work on you that could be cleared up in a few symbols.

I have fallen in love with specifying each new function in my teaching with not only the input and output spaces but also the canonical notation for input point and output point.

---

Bundle all the things 🤠

We all need more fiber in our diets.
