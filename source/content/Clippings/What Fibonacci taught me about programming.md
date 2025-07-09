---
title: "What Fibonacci taught me about programming | Javalobby"
source: "https://web.archive.org/web/20140319112004/http://java.dzone.com/articles/what-fibonacci-taught-me-about"
author:
published:
created: 2025-07-08
description: "I originally wanted to write this neat piece on how solving the “get a number from the Fibonacci sequence” problem can teach YOU a lot but over the past..."
tags:
  - "clippings"
---
The Wayback Machine - https://web.archive.org/web/20140319112004/http://java.dzone.com:80/articles/what-fibonacci-taught-me-about

## What Fibonacci taught me about programming

I originally wanted to write this neat piece on how solving the “get a number from the Fibonacci sequence” problem can teach YOU a lot but over the past year, I’ve realized that programming is such a personal experience that I believe I’d do you injustice by preaching and schooling you.

Instead, I’d like to focus on my own experience with it.

A few weeks ago, I was solving the Fibonacci sequence problem:

> Given an index, return the correct number from the Fibonacci sequence.

I tried different approaches, looked up how others have done it and learn a few awesome things.

## Recursion is badass but can be misleading

One solution that I’ve seen was the recursive one. Recursion to me has always been magic. Partially because you have to approach a problem with a certain mindset to be able to use recursion. And I rarely ever find problems that require that mindset.

Anyways, so I found a solution and just looking at it, I thought that it was the best thing ever.

First, let me show you the functional (mathematically functional) representation of Fibonacci:

```js
F(n) = F(n-1) + F(n-2)
```

Basically, each Fibonacci number is equal to the sum of its two predecessors. The recursive solution looks very much like the mathematical representation:

```js
function fibRec(i) {
  if (i < 2) {
    return i;
  } else {
    return ( fibRec(i-1) + fibRec(i-2));
  }
}
```

I thought to myself, “This is perfect! So simple, and it describes itself! This MUST be the perfect solution!” but it’s not. Look at what happens when you run this neat recursive function:

![fibonacci-recursion](https://web.archive.org/web/20140319112004im_/http://cdn.antjanus.com/wp-content/uploads/2014/03/fibonacci-recursion.jpg)

As you can see, the function gets recursively worse in terms of performance. We’re exponentially calculating the same equation. I’d call this the “near-infinite loop”. Because we calculate and recalculate the same problem over and over and over. The larger our `i` gets, the more exponentially worse the recursion gets.

So I reminded myself of an old saying:

> just because it looks right, it doesn’t mean it is.

I learned that not every problem that looks like a recursion-solvable should be solved with recursion. Technically, this is a prime example of where recursion mirrors the nature of the problem but is not a good solution.

## Then comes solving programmatically (or Naive)

Every problem out there has an inelegant “naive” solution. I say “naive” because it’s seemingly inefficient. For instance, the solution to Fibonacci using plain programming is this:

```js
//programmatically
function fibProg(i) {
  var a = 0;
  var b = 0;
  var c = 0;

  for(var d = 0; d < i+1; d++) {
    if(d === 1) {
      c = 1;
    } else {
      c = a+b;
    }
    a = b;
    b = c;
  }

  return c;
}
```

As you can see, we have to count up from 0 all the way up to the index every single time. It’s terribly inefficient. Isn’t there a way to just “skip” to the correct number instead of this iterative approach? No, not with just programming. However, the solution is performant enough that you can leave it at that. No need to go further.

The recursion solution could result in maximum call stack errors, overflows, and what have you. This solution won’t and it will work efficiently up to some arbitrary high number.

### The Mathematical Solution

Being a former math major, I remembered that there is a Fibonacci solving formula based on the golden ratio. A quick look up in Wikipedia resulted in a sweetly simple equation:

[![fib-equation](https://web.archive.org/web/20140319112004im_/http://cdn.antjanus.com/wp-content/uploads/2014/03/fib-equation.jpg)](https://web.archive.org/web/20140319112004/http://cdn.antjanus.com/wp-content/uploads/2014/03/fib-equation.jpg)

I decided to plug it into a function and create a `fibMath` function for a solution:

```js
function fibMath(i) {
  var sqrtFive = Math.sqrt(5);
  var firstHalf = 0;
  var secondHalf = 0;

  firstHalf = 1 / sqrtFive * Math.pow( ( ( 1 + sqrtFive ) / 2), i);
  secondHalf = 1 / sqrtFive * Math.pow( ( (1 - sqrtFive ) / 2 ), i);
  return Math.round(firstHalf - secondHalf);
}
```

It’s a pretty neat but completely un-understandable function for a programmer. However, the performance is staggering.

I love how math can cut through problems like butter through innovative formulas. I was taken aback and realized that there are things about programming on the fundamental, mathematical level that I may not fully understand but allow us to work at the speeds we work at.

**Note:** Someone pointed out to me that the Math.round() function will eventually end up with incorrect solutions due to the floating point error and similar problems. There are some [workarounds](https://web.archive.org/web/20140319112004/http://stackoverflow.com/questions/1458633/elegant-workaround-for-javascript-floating-point-number-problem) if you need to be precise and will be using this function out in the real world.

### The Tests

I decided to test all of the solutions with [JSPerf](https://web.archive.org/web/20140319112004/http://jsperf.com/), a cool little app that employs [Benchmark.js](https://web.archive.org/web/20140319112004/http://benchmarkjs.com/) for benchmarking.

I set up as fair of a test as I could and put all three solutions to work.

First up is a benchmark that allows `fibRec` (the recursive solution) to be used. I found that the `maximum call` error pops up in the range of 50 or above (perhaps even lower). So I started with getting the 20th index.

[Check it out](https://web.archive.org/web/20140319112004/http://jsperf.com/fibonacci-solutions). Here are the results for my computer:

![fib-benchmark-1](https://web.archive.org/web/20140319112004im_/http://cdn.antjanus.com/wp-content/uploads/2014/03/fib-benchmark-1.jpg)

To further test the programmatical vs mathematical solutions, I picked a higher index to compute in a “hardcore mode”.

[Check that out](https://web.archive.org/web/20140319112004/http://jsperf.com/fibonacci-solutions-hardcore-mode) and see the difference:

![fib-benchmark-2](https://web.archive.org/web/20140319112004im_/http://cdn.antjanus.com/wp-content/uploads/2014/03/fib-benchmark-2.jpg)

Note that this hardcore mode tests for the index of 54320 instead of 20. What’s interesting is that while the mathematical solution is much MORE performant, the programmatical solution works just fine. Unless I’m directly dealing with math solutions, there’s no need to go nuclear and convert functions into mathematical representations (although, that would be a neat project).

I believe that game programming relies on mathematical formulas due to these difference, however, they do actually run these equations several million times a second.

### So I learned about optimization

The difference between the programming solution and the mathematical solution reminds me of the difference of running native assembly code and something like PHP. The math solution is like magic, and so is assembly (sometimes). But it’s not practical in most cases, in terms of debugging, understanding, and changing.

The entire process taught me that it’s important to avoid potential bottlenecks like the first solution but it’s just as important to not get hung-up at the performance of solutions like the programming solution. I thought it was going to be slow but I was wrong. At 2000 ops/sec with a very high look up index, there was nothing to worry about whatsoever. That’s a performant solution.

Could I do better? Yeah. And I did, the mathematical solution gave me performance several times over the programming one. And if I was using Fibonacci or other mathematical concepts out in the real world, I would have learned my lesson to use the smart way and not the “manual” way (manual, as in, the computer manually computes a solution rather than cutting straight through to the answer).

The downside to the math solution is that it’s not often available for most real-world problems (outside of video gaming and 3D). The non-math solution is good enough though and should not be dismissed.

On the other hand, a less performant but understandable/maintanable solution is much better than a very performant yet illegible is a trap that should be avoided.

I don’t know if that makes sense, but it was an interesting exercise.

Published at DZone with permission of [Antonin Januska](https://web.archive.org/web/20140319112004/http://java.dzone.com/users/antjanus), author and DZone MVB.  