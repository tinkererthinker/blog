---
title: "Discovering a formula for the cubic"
source: "https://gowers.wordpress.com/2007/09/15/discovering-a-formula-for-the-cubic/"
author:
  - "[[Gowers's Weblog]]"
published: 2007-09-15
created: 2025-01-31
description: "In this post I want to revisit a topic that I first discussed on my web page here. My aim was to present a way in which one might discover a solution to the cubic without just being told it. However, the solution that arose was not very nice, and at the end I made…"
tags:
  - "clippings"
---
In this post I want to revisit a topic that I first discussed on my web page [here](http://www.dpmms.cam.ac.uk/~wtg10/cubic.html). My aim was to present a way in which one might discover a solution to the cubic without just being told it. However, the solution that arose was not very nice, and at the end I made the comment that I did not know a way of removing the rabbit-out-of-a-hat feeling that the usual much neater formula for the cubic (together with its derivation) left me with.

A couple of years ago, I put that situation right by stumbling on a very simple idea about quadratic equations that generalizes easily to cubics. More to the point, the stumble wasn’t completely random, so the entire approach can be justified as the result of standard and easy research strategies. I am no historian, but I would imagine that this idea is pretty similar to the idea (in some equivalent form) that first led to this solution.

I shall assume familiarity with solving quadratics-the problem here is to find the right way of generalizing this solution. (If you want to see how one might discover a solution to the quadratic then I cover that in the earlier discussion of cubics.) Given that, then the first step in a natural discovery of a solution of the cubic is the observation, which one can hardly help making, that solutions to quadratics take the form $u \pm \sqrt{v}$. If we now turn things round and just assume that solutions will take this form then we can get a very quick derivation of the quadratic formula, which, for simplicity, I will do just for quadratics of the form $x^2+b x+c$. (Of course, it is very easy to reduce the general case to this case, so this is not a serious loss of generality.)

The derivation comes from the well-known fact that the roots of such a quadratic must add up to $-b$ and must multiply to give $c$. The first fact tells us that $u=-b / 2$ and the second tells us that $(u+\sqrt{v})(u-\sqrt{v})=c$, which in turn tells us that $u^2-v=c$, so that $v=u^2-c$. By our earlier computation, this is $b^2 / 4-c$. This gives the usual quadratic formula in the case $a=1$.

Was that a fully justified argument? Yes, because once you are looking for roots of the form $u \pm \sqrt{v}$ there is no mystery behind the idea of looking at what you know about the two roots, converting that into some equations for $u$ and $v$ and trying to solve those equations. You can't tell in advance that the equations will have a nice solution, but it's very natural to give the approach a try.

Now let us ask ourselves the following question: what would be the most blindingly obvious way of generalizing the above approach to cubics? There are two ideas we might have in connection with this. The first is to try to get the cubic into as simple a form as possible, and the second is to make a guess about the general form of the roots. Let us take each of these in turn, beginning with the second.

What is the most natural way of generalizing our choice above for the form of the roots? To ask this question another way: we are trying to find XXX , where XXX is to the number 3 as $u+\sqrt{v}$ and $u-\sqrt{v}$ are to the number 2 . There is a very obvious guess: we should take $u+r, u+s$ and $u+t$, where $r, s$ and $t$ are the three cube roots of some number $v$. If we write $\omega$ for the cube root of 1 (or, to be more specific, the number $e^{2 \pi i / 3}$, then we can write this guess as $u+v^{1 / 3}, u+\omega v^{1 / 3}$ and $u+\omega^2 v^{1 / 3}$ (where $v^{1 / 3}$ is some cube root of $v$-it doesn't matter which).

By analogy with the quadratic case, we are hoping that this will be the general form of a solution to the equation $x^3+b x^2+c x+d=0$. But a moment's thought shows that it cannot be. Let us see this in two different ways.

The first is that if that is the general form of the roots, then we have two degrees of freedom-the choice of $u$ and the choice of $v$. But we are looking at a three-dimensional set of equations (since we are free to choose $b, c$ and $d$ ). It is a good exercise to prove rigorously that our guess is guaranteed to be wrong for this reason, but for now let us be satisfied with the observation that it looks very worrying. Indeed, if life were that simple then it is hardly likely that solving the cubic would have been as hard a problem as it was.

A second way to see that the guess is wrong is to consider what happens if $b=0$. Now we are looking at a cubic of the form $x^3+c x+d$, and if the roots take the form stated then, since their sum is now zero, we find that $u=0$. But then the three roots are just the cube roots of $v$, so they are the roots of the equation $x^3-v=0$. In other words, the guess is wrong unless $c=0$. (This is of course an instance of the fact that we do not have enough degrees of freedom.)

So, with this small extra insight into the problem, let us try to come up with a better guess. How do we generalize a pair such as $u+\sqrt{v}$ and $u-\sqrt{v}$ ? We want a triple of roots, but we also want each component of the triple to have three degrees of freedom. In other words, we want each root to be made out of a $u$, a $v$ and a $w$.

Since we don't quite know how we will build the roots, a helpful idea at this point is to lose some information in the quadratic case. This is a slightly subtle point that I will discuss more in a moment. First let us merely observe that I could have represented the two roots of a quadratic as $u+v$ and $u-v$, and it would still have been very easy to solve for $u$ and $v$. Then the fact that a square root was involved would not have been a guess (however natural) but something that one actually derived, in a very easy and natural way.

Since this slight modification of the quadratic guess will turn out to be very helpful, it is important to establish that it could be justified. That is, I am not drawing a rabbit out of a hat at _this_ point. The justification is as follows. In the cubic case we do not know exactly what the form of our guess would take. We could just make some _wild_ guesses and hope to hit the right answer. But much better is to make more _general_ guesses and then _work out_ what their more precise forms must be. We can do that in the quadratic case, so it is a very sensible strategy to try to do the same for cubics.

Having established this point, let us see what happens. We are now trying to find the natural analogue for the number 3 , built out of three variables $u, v$ and $w$, of the pair $(u+v, u-v)$ in the degree- 2 case. The pair $(u+v, u-v)$ consists of a couple of linear combinations of $u$ and $v$, so it is natural (though not essential to the discovery of the argument) to think of it as a linear transformation of the pair $(u, v)$. That draws our attention to the matrix $\left(\begin{array}{cc}1 & 1 \\ 1 & -1\end{array}\right)$, and it is then very natural to wonder if this matrix has an obvious generalization to a $3 \times 3$ matrix.

It does! This is the $2 \times 2$ case of the well-known circulant matrix, but even if you don't know that, you do know that the numbers 1 and -1 are the two square roots of 1 . Moreover, this is not just a coincidence but the reason that they occur in our discussion of quadratics. So it is natural to try to build a $3 \times 3$ matrix out of the three cube roots of 1 , which are $1, \omega$ and $\omega^2$. In the end there is only one sensible choice to make (give or take the odd symmetry). It is the matrix $\left(\begin{array}{ccc}1 & 1 & 1 \\ 1 & \omega & \omega^2 \\ 1 & \omega^2 & \omega\end{array}\right)$. Thus, our guess for the forms of the three roots is $u+v+w, u+\omega v+\omega^2 w$ and $u+\omega^2 v+\omega w$.

This seems a very satisfactory guess (even if we don't have a compelling reason to suppose that it will work). So now we are left with the task of solving for $u, v$ and $w$ on the assumption that they are the roots of the cubic $x^3+b x^2+c x+d$. At this point one could just plunge in, but it helps a lot to simplify the cubic first by "completing the cube". This is the familiar idea (described in my other cubics discussion) that by substituting $y=x+b / 3$ for $x$ you get a cubic in $y$ where the coefficient of $y^2$ is zero. So let's just assume, as we may, that $b=0$, so that we are looking for roots of $x^3+c x+d$. Since the roots add up to 0 and $1+\omega+\omega^2=0$, this tells us that $u=0$, so the three roots are now of the form $v+w, \omega v+\omega^2 w$ and $\omega^2 v+\omega w$. (We are therefore down to two degrees of freedom, but so is the cubic we are trying to solve.)

The information we know about these three roots is that their product is $-d$ and that the sum of all the products of two of them is $c$. So the next task is clear: expand out these expressions and see if we can solve the resulting equations in $u$ and $v$. The details of this are not particularly important: you could stop reading now and just take on trust that we end up needing to solve quadratics and take cube roots, both of which we are allowed to assume that we can do. However, it's nice to see that it really does work.

The product of the three numbers $v+w, \omega v+\omega^2 w$ and $\omega^2 v+\omega w$ works out to be $v^3+w^3$. (It's instructive to do this calculation for yourself and see how the fact that $1+\omega+\omega^2=0$ makes the other two possible terms cancel. Then one can see that the fact that rather simple expressions come out of these calculations is not a coincidence.) As for the sum of the three products of two of them, it comes out to be $3\left(\omega+\omega^2\right) v w$, which equals $-3 v w$. So we need $-3 v w$ and $v^3+w^3$ to take the values $c$ and $d$, respectively. This tells us that $v^3$ and $w^3$ are the two roots of the equation $x^2-d x-c^3 / 27=0$, so, as claimed, we can solve for $v$ and $w$ by solving a quadratic and taking cube roots.

A small extra point is that one must think a bit about which cube roots to take, but that I will gloss over here.

An obvious question: what happens if one tries to generalize this approach to quartics and quintics? The answer is that in both cases it is obvious how to generalize the guess about the form that the roots should take. In the case of the quartic, when one guesses that they are of the form $u+v+w+t, \quad u+i v-w-i t, \quad u-v+w-t$ and $u-i v-w+i t$, everything works out nicely, if you get rid of the $x^3$ term and hence of $u$. You get some equations in $v, w$ and $t$ and they aren't too hard to solve. If you try it for the quintic then, not too surprisingly, you end up with some equations that are more complicated than the quintic you started with.

## Comments

[[Terence Tao]]
- It is amusing to recast your above discussion through the lens of Fourier analysis. One can view solving a polynomial as solving a system of [[Symmetric Equations | symmetrised equations]]. For instance, by the factor theorem, the task of finding the three roots $x, y, z$ of the cubic $x^3+b x^2+c x+d=0$ is equivalent to solving the system of equations
$$
\begin{aligned}
& x+y+z=-b \\
& x y+y z+x z=c \\
& x y z=-d
\end{aligned}
$$
- Now these equations are invariant under cyclic shift of the $x, y, z$. One of the key insights of Fourier analysis is that any mathematical problem which enjoys a translation invariance symmetry is likely to be clarified by use of the Fourier transform. This would motivate the Fourier substitution $x=u+v+w$, $y=u+\omega v+\omega^2 w, z=u+\omega^2 v+\omega w$, which leads to
$$
\begin{aligned}
& 3 u=-b \\
& 3 u^2+3 v w=c \\
& u^3+v^3+w^3-3 u v w=-d
\end{aligned}
$$
- This lets one solve for $u$; to solve for $v$ and $w$ one can then observe a residual cyclic symmetry between $v$ and $w$, prompting another Fourier transform $v=s+t, w=s-t$, which soon lets one solve for everything.
- Presumably this can all be interpreted nicely in terms of the Galois group $S_3$, and in particular to the solvability of that group, especially given that solvable groups can be "built up" from abelian groups such as $\mathbb{Z} / 3 \mathbb{Z}$ and $\mathbb{Z} / 2 \mathbb{Z}$, which are precisely the groups which enjoy nice Fourier transforms. My [[Galois theory]] is incredibly rusty, though, so I don't see the connection clearly.
- By some coincidence, there is another blog post on the solvability of the cubic, this time from the perspective of classical invariant theory, at
  https://rigtriv.wordpress.com/2007/08/29/invariants-and-solving-polynomials/
	- Basically, the philosophy here is to only permit yourself to write down expressions (such as the discriminant) which transform nicely under projective changes of coordinates. There are relatively few of these expressions, and so you have a smaller “search space” in which to find the invariants that factorise the original polynomial into linear factors.
	- [[Geometry of a Polynomial]]

gregknese
- I really enjoyed this post and the discussions afterwards. It seems many people are rusty on Galois theory. Every time I have learned Galois theory (and then promptly forgotten it) I always left feeling that it is an amazing theory but I would never know how to use it to solve a concrete question. For example: If one knows that a given quintic is solvable by radicals, how does one go from there and actually find the roots? Any thoughts?

JOHN SMITH
- It was stated on your home page that any reasonable person wouldn’t be expected to solve the cubic in a few hours or so. However, how long would you expect say a cambridge undergraduate with no knowledge of solving the cubic to discover the solution?

gowers
- My answer to JOHN SMITH’s first question of September 18th is that I would expect most Cambridge undergraduates _not_ to manage to find a solution to the cubic unaided. However, that is not because they would be incapable of it. My post tries to demonstrate that by showing that you don’t have to have flashes of genius to solve the cubic — just the wish to generalize the quadratic solution in as natural a way as you can. Rather, it is because only a smallish proportion of Cambridge undergraduates (or indeed, mathematics undergraduates anywhere) start out with the belief that they could ever solve a mathematics problem that wasn’t carefully constructed to be solvable in a fairly routine way. There’s a simple way of getting this belief, which is to solve one hard problem. It may take a few hours, or a week, or a month, or six months, or even longer, but once someone has done it they understand from their own experience that it is possible. Then they start to have positive thoughts like, “What strategy will maximize my chances of solving this problem?” or “I seem to keep having the same difficulty — what could I do differently?” rather than negative ones like, “Maths is hard, and I haven’t been taught how to do this, so there’s no chance of my managing.” And then they find that solving difficult problems is just like many other activities: hard, yes, but not impossible and something that gets easier with practice.

Issa Rice
- The matrices given in the post don’t seem to be circulant matrices (as defined in places like Wikipedia). Instead, the matrices seem to be what Wikipedia calls the (unnormalized) DFT matrix. There does seem to be a connection between the two types of matrices, however: the columns of the DFT matrix are the eigenvectors of the circulant matrix.
- On a related note, even after figuring out the pattern for the matrices, it is still not at all clear to me how I would have guessed that this was what was going on after staring at the ![2 \times 2](https://s0.wp.com/latex.php?latex=2+%5Ctimes+2&bg=ffffff&fg=333333&s=0&c=20201002) case. In other words, after seeing the ![2 \times 2](https://s0.wp.com/latex.php?latex=2+%5Ctimes+2&bg=ffffff&fg=333333&s=0&c=20201002) matrix my first (or even twentieth) thought wouldn’t be “hey, that’s just the DFT matrix”. The post says “In the end there is only one sensible choice to make”, but I wonder if you could elaborate on what thought processes would lead to this choice.