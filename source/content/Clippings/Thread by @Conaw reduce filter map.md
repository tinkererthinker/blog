---
title: "Thread by @Conaw"
source: "https://x.com/Conaw/status/1134173309547950081"
author:
  - "[[@Conaw]]"
published: 2019-05-30
created: 2025-05-18
description:
tags:
  - "clippings"
---
**Conor White-Sullivan 𐃏** @Conaw [2019-05-30](https://x.com/Conaw/status/1134173307878629376)

Reduce. Filter. Map.

I first learned to code for the same reason I learned foreign languages. I was promised it would change the way I think.

Those three functions for transforming lists delivered so thoroughly it's hard to think without them.

Algorithms of thought.

---

**Conor White-Sullivan 𐃏** @Conaw [2019-05-30](https://x.com/Conaw/status/1134173308704907264)

Reduce:

Take a list, an accumulator, and a function that looks at each item in the list one at a time, and the current value of the accumulator, and transforms the accumulator to pass on to the next value in the list.

Can produce a new list, or just find a single value

---

**Conor White-Sullivan 𐃏** @Conaw [2019-05-30](https://x.com/Conaw/status/1134173309547950081)

Map and Filter are both built out of reduce

---

**Conor White-Sullivan 𐃏** @Conaw [2019-05-30](https://x.com/Conaw/status/1134173310298681344)

Filter -- take a list, and a test, return only the items of the list that meet the test criteria

---

**Conor White-Sullivan 𐃏** @Conaw [2019-05-30](https://x.com/Conaw/status/1134173311166951424)

Map -- take a list, and a transformation function, return a new list

---

**Conor White-Sullivan 𐃏** @Conaw [2019-05-30](https://x.com/Conaw/status/1134173311909355520)

In practice -- for notes

Filter your notes for questions

Map over your open questions and say

\-- how could I reframe this question to make it easier to answer

\-- what smaller or bigger questions help me answer this one

\-- how will I know I've found an answer

---

**Conor White-Sullivan 𐃏** @Conaw [2019-05-30](https://x.com/Conaw/status/1134173312743923713)

Filter your notes for beliefs

Map over them

Ask

\-- How surprised would I be if this were false ("weight")

\-- what other beliefs do I think are true because this one is \*what does this imply\*

\-- What other beliefs, if I changed my mind about them, would change this one

---

**Conor White-Sullivan 𐃏** @Conaw [2019-05-30](https://x.com/Conaw/status/1134177043866775552)

Even computer threads look at items in a list one at a time. They just do it quickly.

No shame in doing the same

---

**braai engineer** @PetrusTheron [2021-05-06](https://x.com/PetrusTheron/status/1390334498026426371)

What’s interesting about filter is that it has a shorter output type coz rejected items consume cycles even when going to “the bin”. For input seq, time between lazy filter emissions can be surprising. I like to think of filter as split or partition into two piles, one hidden.