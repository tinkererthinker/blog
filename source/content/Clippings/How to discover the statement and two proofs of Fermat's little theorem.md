---
title: How to discover the statement and two proofs of Fermat's little theorem
source: https://www.dpmms.cam.ac.uk/~wtg10/fermat.html
author:
  - Timothy Gowers
published: 
created: 2025-01-31
description: 
tags:
  - clippings
---
## How to discover the statement and two proofs of Fermat's little theorem

## The statement, and sketches of the usual proofs

Fermat's little theorem states that if p is a prime and x is an integer not divisible by p, then x<sup>p-1</sup> is congruent to 1 (mod p).

One proof is to note that x can be regarded as an element of the multiplicative group of non-zero residue classes (mod p). It generates a cyclic subgroup, and the order of that subgroup is the minimal r such that x<sup>r</sup>\=1 (mod p). By Lagrange's theorem, this r must divide p-1, from which the theorem readily follows.

Another proof is to deal with a modified statement: that x<sup>p</sup>\=x (mod p) for every x. This implies the first version, since when x is non-zero (mod p) one can divide through by x. This modified statement is proved by induction. If x<sup>p</sup> is congruent to x, then expanding (x+1)<sup>p</sup> by the binomial theorem, we obtain the sum

x<sup>p</sup>+(pC1)x<sup>p-1</sup>+...+(pCr)x<sup>p-r</sup>+... +(pCp-1)x+1.

It is not hard to show that (pCr) (my notation while writing in HTML for the binomial coefficient p choose r) is divisible by p for every r between 1 and p-1 inclusive, which tells us that (x+1)<sup>p</sup> is congruent to x<sup>p</sup>+1. By the inductive hypothesis, this is congruent to x+1, as was needed.

## Prerequisites

I shall assume some familiarity with modular arithmetic. It is not too hard to see how such familiarity could arise. For example, when thinking about Diophantine equations, it is very natural to consider whether the variables are even or odd, and then natural to generalize from this to their values to a higher modulus. (A good example is the Diophantine equation x<sup>2</sup>\=2y<sup>2</sup>, which, famously, has no solution other than x=y=0.) Initially, one might say "let n=5m+a, where a=0,1,2,3 or 4," but sooner or later one would realize that one was not interested in m.

## Thinking of the statement.

It is easy to imagine thinking of the statement of the fundamental theorem of arithmetic. After learning to multiply integers, one would soon see that some had many factors and others none, and it does not take much insight to see that every number has a factorization into primes, or much curiosity to ask whether this is unique (unless one falls into the trap of thinking that it is too obvious to need a proof). Fermat's little theorem is rather different, however. It seems almost magic that it is true, and a little mysterious that it was noticed before group theory came along and made it fairly obvious.

However, perhaps it is not as mysterious as all that. If modular arithmetic was discovered as a result of [[Diophantine equations]], or at least used to discuss them, then there was plenty of reason to consider sequences of the form 1, x, x<sup>2</sup>, x<sup>3</sup>, .... (mod p). A very small amount of experiment would reveal that these sequences are periodic (a fact one notices when looking at the powers of a number in their base 10 representation), and the proof that they are periodic is very simple.

Now one can hardly avoid asking the question, "What is the period?" The proof that the sequence is periodic also yields the fact that the period is equal to the number of distinct values taken by the powers of x, provided that there is some non-zero m for which x<sup>m</sup>\=1. If p is a prime, then it is a well known fact that numbers that are non-zero (mod p) have multiplicative inverses (a reformulation of one of the main lemmas used to prove unique factorization) from which it is easy to deduce that the first repeat of the sequence is indeed at some m such that x<sup>m</sup>\=1.

At this point, it is natural to try some small examples. The powers of 2 (mod 7) are 1,2,4,1,2,4,1,2,4,... and the powers of 3 are 1,3,2,6,4,5,1,3,2,6,4,5,.... . This is already instructive. We see that the period of the powers of three is twice that of the powers of 2, basically because 3<sup>2</sup>\=2. In fact, once we see that the powers of 3 include all non-zero numbers (mod 7) (or in modern language, that 3 is a generator of the multiplicative group (mod 7), we see that we can read off the period of the sequence associated with any of the numbers, just by jumping along the sequence 1,3,2,6,4,5,1,3,2,6,4,5,... by regular amounts.

\[Perhaps the reasoning of the above paragraph relies a little too much on human intelligence. However, it can be broken down further. For example, a sensible computer would ask whether there was any relationship between the two sequences above. A very rudimentary pattern-recogniser would be enough for it to spot that every other power of three is a power of two. It could then ask what conditions must be satisfied for something like this to happen.\]

It is now clear that the period of every sequence of powers (mod 7) is a factor of 6, and it is natural to wonder whether the same argument works for every other p. For this one needs a generator. So we have proved the following. If there is some y such that the powers of y exhaust all non-zero residues (mod p) then x<sup>p-1</sup>\=1 (mod p) for every non-zero x.

\[Once again, the reasoning can be broken into yet smaller parts. Why is it clear that the period of every sequence of powers (mod 7) is a factor of 6? Because by now we have realized (as a result of trying to generalize from our experience with the number 2) that every number can be written as 3<sup>t</sup>, which implies that its sixth power is 3<sup>6t</sup>\=(3<sup>6</sup>)<sup>t</sup>\=1 (mod 7). In these pages, I shall sometimes miss out the details of how to discover arguments that are much simpler to work out than the main argument.\]

## Finding the group-theoretic proof

It is very tempting to try to finish the argument that I have just started, by trying to prove that there must be an element that generates the multiplicative group (mod p). However, let me assume, slightly unrealistically, that we have decided to ignore that approach for now, and are simply going to regard the statement x<sup>p-1</sup>\=1 (mod p) as given to us out of the blue to be proved.

Thus, what we are trying to prove is the following statement. Let p be a prime. Then the set A of distinct values taken by the powers of any given non-zero x (mod p) has cardinality dividing p-1. Let us apply the following principle.

#### Principle 1.

*If you are trying to prove something about some numbers that arise in a problem, then see what significance can be attached to those numbers.*

One of the numbers in this problem is p-1. Does it have any significance? Well, yes it does because p has an obvious significance and p-1 is just p with 1 subtracted. However, we should still ask why subtracting 1 is a natural thing to do. For example, is there any set around with p-1 elements? Yes there is: the set of non-zero residues (mod p), which also has an obvious significance to the problem.

This guides us to the following small reformulation of the problem: let A be the set of powers of x and let B be the set of all non-zero residues. Then the size of A divides the size of B.

#### Principle 2.

*Drop some of the hypotheses just to get a general picture of what a successful proof might look like.*

We could consider the following very general (and ill-posed) problem: let A and B be two sets - prove that the size of A divides the size of B. How can we do this? Obviously we shall need more hypotheses later, but the following general method springs to mind straight away: work out how many elements A has and how many elements B has, divide the second number by the first and show that the answer is an integer.

Now let us return to the actual example and try to carry out this programme. We run into an immediate problem, which is that we cannot work out how many elements A has, because the size of A depends on x. Worse still, it depends on x in a way that is hard to understand.

This insight provokes us to reformulate the general problem slightly as follows: let A and B be two sets - prove that the size of A divides the size of B, even though the size of A is unknown. This looks strange, so let us see if we can change the problem slightly. We are trying to show that |B|=k|A| for some k. Why don't we consider the following closely related problem: let A and B be sets; prove that they have the same cardinality, even though this cardinality is unknown. (This problem was arrived at by setting k=1 and noticing that if the cardinality of A was unknown then the cardinality of B had better be unknown as well.) Finally, we have a new idea: try to construct a bijection between A and B. \[This would occur to a computer because of its associations with the word \`cardinality'.\]

Recognising that we have a new insight, we return to the problem of showing that the cardinality of A divides that of B. The statement that |B|=k|A| is equivalent to the statement that there is a bijection between B and k copies of A. More formally, it is the same as saying that there are injections f\_1,...,f\_k from A to B with disjoint images.

How might we find such injections in the case we are actually interested in? One approach we can quickly dismiss is to prove their existence indirectly, since the mere statement that the injections exist is absolutely equivalent to what we are trying to prove, namely that |A| divides |B|. (Thus, we are not exactly dismissing the idea, but simply observing that if we try this approach then we are back where we started, so it might be better to try something with a chance of being new.)

It is clear, then, that we should be trying to *construct* the injections f<sub>1</sub>,...,f<sub>k</sub>. Let us do the usual thing, and simplify the problem. We could ask ourselves whether we can see how to construct any injection from A to B at all. Since in this case A is a subset of B, the answer is easy - just map an element x<sup>t</sup> of A to itself.

Let us try to build up from here. The next step is to look for a second injection from A to B with image disjoint from A (which is the image of the first). How could we possibly construct a second injection?

#### Principle 3.

*Write down what you know and see what you can do with it.*

In this case, we are trying to construct a function. Are there any functions around? Yes there are, since addition and multiplication (mod p) are both functions. Unfortunately, they are binary operations, whereas we are looking for a unary operation. Still, let us ask ourselves the following: given a binary operation, how can one construct from it a unary operation - that is, a normal function? There is one very natural answer, which is to fix one of the variables. Thinking a little more, we realize that multiplication is more suitable for our purposes than addition, since B is closed under multiplication and not under addition. Thus, by a process of looking for the simplest construction that uses what we know and doesn't obviously not work, we arrive at the following question: does there exist some b in B (that is, some non-zero b (mod p)) such that the set of all bx<sup>t</sup> is disjoint from the set of all x<sup>t</sup>?

#### Principle 4.

*Try something and work out what happens if it fails.*

At this point we could try setting b=2, or we could simply see what happens for a general b. If we do the second, then failure is equivalent to the statement that there exist r and s such that bx<sup>r</sup>\=x<sup>s</sup>. If we simplify this, then it tells us that b=x<sup>s-r</sup>, and in particular, that b belongs to A. \[In fact, that \`in particular' is more like an equivalence, since r and s are hypothetical (that is, could be anything), so all we know about b is that it belongs to A.\]

Hence, if we can find some b that does not belong to A, then we have constructed the desired injection. If, on the other hand, we cannot find such a b, then A=B and the theorem is proved.

Now we continue. We would like to find a third injection, with image disjoint from A and also disjoint from bA. We would be mad not to try cA for some c. We know from the discussion about b that cA is disjoint from A if c does not belong to A (and it is easy to see that the converse is true as well). Under what conditions will cA and bA be disjoint? Well, cA intersects bA if and only if there exist r and s such that cx<sup>r</sup>\=bx<sup>s</sup>, which implies that c=bx<sup>s-r</sup> and therefore belongs to bA.

Thus, we are searching for c that belongs neither to A nor to bA. If such a c does not exist, then B is the disjoint union of A and bA, which implies that |B|=2|A| and the theorem is proved. Otherwise, we have found our c.

We now need a principle that tells us to get bored with the above process and try to extract from it a general (inductive) argument. Something like the following will do.

#### Principle 5.

*If you are trying to construct a sequence x<sub>1</sub>...x<sub>k</sub> and k is a hypothetical integer, as opposed to something fixed like 100, then you cannot do it by constructing x<sub>1</sub>, then x<sub>2</sub>, then x<sub>3</sub> and so on, all by separate arguments, since then the proof has hypothetical length! One way to do it is by induction. (In fact, induction may well also be useful if k is fixed, but large.)*

It is a fairly automatic process to set up an inductive argument in this case. We assume that we have found injections f<sub>1</sub>,...,f<sub>j</sub> by our method, which means that, for each i, f<sub>i</sub> multiplies an element of A by some c<sub>i</sub>. We would like to find c<sub>i+1</sub> and hence f<sub>i+1</sub>. The condition is that it should not belong to any of the sets c<sub>i</sub>A. If we cannot find an element of B satisfying this condition, then |B|=j|A| and we are done. Otherwise the sequence continues. Eventually, since B is finite, this process ends, and the theorem is proved.

Notice that it is not a big leap from this theorem to proving Lagrange's theorem. \[Perhaps the hardest thing for a computer - it was certainly hard for humans - would be to spot that multiplication does not have to be commutative. For this it would need to think abstractly about binary operations and pick out the property of commutativity. A more plausible route to Lagrange's theorem in its full generality could well be via geometry and symmetries.\]

## Finding the proof via binomial coefficients

The first obstacle that must be overcome is that one is proving a modified statement. What is more, the assertion that x<sup>p</sup> is congruent to x is less natural, especially if one has seen the group-theoretic proof, than the assertion that x<sup>p-1</sup> is congruent to 1. How, then, is one supposed to think of the reformulation?

I have two answers to this question. They both start with the idea of trying an inductive proof. If one is going to do this, then what should the inductive hypothesis be? Presumably, it will be that x<sup>p-1</sup> is congruent to 1, which we know to be true when x=1. However, we also know it to be *false* when x is divisible by p, so the best we can hope for is that we will find an inductive argument that breaks down at p.

This does not seem all that natural, though it is not obviously impossible. The first thought that leads to the reformulation is that it would be better to try to find a \`single statement' (as opposed to splitting into the two cases \`p divides x' and \`p does not divide x') that would serve as a better inductive hypothesis. Then, after a little trial and error, one arrives at x<sup>p</sup> being congruent to x.

A more involved, but more satisfactory way of arriving at the reformulation (satisfactory because it does not assume much imagination) is as follows. Let us simply try to go ahead with an inductive proof of the original statement and see what happens. Assuming that x<sup>p-1</sup> is congruent to 1, what can we say about (x+1)<sup>p-1</sup>? A natural thing to do (especially in the absence of any other ideas) is to expand using the binomial theorem, obtaining

x<sup>p-1</sup>+(p-1C1)x<sup>p-2</sup>+...+(p-1Cr)x<sup>p-3</sup>+... +(p-1Cp-2)x+1.

It is very encouraging that the first term of this expansion is x<sup>p-1</sup>. How can we prove that the rest adds to zero (mod p)? We cannot expect to simplify it using the binomial theorem, since we would end up with (x+1)<sup>p-1</sup>\-x<sup>p-1</sup> and be back where we started. Therefore, we have little choice but to examine it term by term. We observe first that (p-1C1) is congruent to -1. What about (p-1C2)? This is (p-1)(p-2)/1.2, and this is congruent to (-1)(-2)/1.2 which equals 1. In fact, a simple pattern is appearing: (p-1Cr) equals (p-1)(p-2)..(p-r)/1.2...r which is congruent to (-1)<sup>r</sup>.

This looks very promising indeed, because *something is going on* . Perhaps another principle is in order.

#### Principle 6.

*If a simplification occurs in one's algebra, there is almost always a reason for it. More generally, there is no such thing as a coincidence in mathematics.*

Even if the second sentence is false, it is still a useful principle. Here, it does not affect what we do, but gives us a nice warm feeling while we are doing it. We rewrite the expansion of (x+1)<sup>p-1</sup> as

x<sup>p-1</sup>\-x<sup>p-2</sup>+...+(-1)<sup>r</sup>x<sup>p-3</sup>+... -x+1.

Can we simplify this further? Of course we can, as it is a geometric progression. It equals (x<sup>p</sup>+1)/(x+1) (at least when p is odd, and the case p=2 is trivial). Actually, that is not quite true when x=-1, but we can at least say that, when we multiply the expression by x+1 we get x<sup>p</sup>+1. So all we have to do now is prove that x+1=x<sup>p</sup>+1, or rather x<sup>p</sup>\=x.

We have arrived at the reformulation. Perhaps a natural reaction at this point would be to recognise that it is obviously equivalent to the original version and think that one had therefore made no progress at all. However, perhaps one would look wistfully at the above argument and realize that the real problem had been that the coefficients of the lower powers of x were not zero. How could one make them zero? We would like to have a p on the top. But then we have to consider coefficients of the form (aCb) with a at least p. It is natural to think of p itself as a value of a, and finally to notice that the reformulation of the problem is genuinely different, not as a statement but *as something to be proved by this method* .

Finally, we assume that x<sup>p</sup> is congruent to x and expand (x+1)<sup>p</sup>, obtaining

x<sup>p</sup>+(pC1)x<sup>p-1</sup>+...+(pCr)x<sup>p-r</sup>+... +(pCp-1)x+1.

This time, (pCr)=p(p-1)..(p-r+1)/1.2...r. As long as r is less than p we really can divide by all of 1,2,...,r. Since p is congruent to zero, the whole coefficient is, and the whole expression simplifies to x<sup>p</sup>+1. By the inductive hypothesis, this is x+1, just as was required.