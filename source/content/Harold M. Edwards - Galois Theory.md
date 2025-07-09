#### Preface

This exposition of Galois theory was originally going to be Chapter 1 of the continuation of my book Fermat's Last Theorem, but it soon outgrew any reasonable bounds for an introductory chapter, and I decided to make it a separate book. However, this decision was prompted by more than just the length. Following the precepts of my sermon "Read the Masters!" [E2], I made the reading of Galois' original memoir a major part of my study of Galois theory, and I saw that the modern treatments of Galois theory lacked much of the simplicity and clarity of the original. Therefore I wanted to write about the theory in a way that would not only explain it, but explain it in terms close enough to Galois' own to make his memoir accessible to the reader, in the same way that I tried to make Riemann's memoir on the zeta function and Kummer's papers on Fermat's Last Theorem accessible in my earlier books, [E1] and [E3]. Clearly I could not do this within the confines of one expository chapter.

And so I decided to write a short book-a sort of volume $1 \frac{1}{2}$ of my work on Fermat's Last Theorem-devoted entirely to the basics of Galois theory. There is very little in this book that is not already to be found, however concisely and however lacking in proof, in Galois. The one major exception is the material on factorization of polynomials (§849-61), which is due to Kronecker and which seems to me to be necessary to give clear meaning to the computations with roots of algebraic equations that Galois and Lagrange performed without inhibition and without comment.

The crux of Galois theory is, appropriately enough, Galois' Proposition I, which is the following characterization of what we call the Galois group of an equation. Let $a, b, c, \ldots$ be the $n$ roots (assumed distinct) of an algebraic equation $f(x)=0$ of degree $n$. The Galois group is a certain subgroup of the group of permutations of the roots $a, b, c, \ldots$ Galois used it to determine whether a given polynomial in the roots $F(a, b, c, \ldots)$ has a known value-in modern parlance, to determine whether $F(a, b, c, \ldots)$ is in the ground field. The characteristic property of the Galois group is that $F(a, b, c, \ldots)$ has a known value if and only if

$$
F(a, b, c, \ldots)=F(S a, S b, S c, \ldots)
$$

for all permutations $S$ of the Galois group. Galois proved the existence and uniqueness of a group with this property by constructing it, using what later became known as a Galois resolvent. (This characterization of the Galois group will be more recognizable to readers familiar with modern formulations of Galois theory after they read the first corollary in §41. See also §63.)

The major theorems of Galois, such as the theorems on the solvability of equations by radicals, flow from the study of the relationship between algebraic equations $f(x)=0$ and the groups associated with them. Of particular importance is the analysis of the way in which the group is reduced when the field of known quantities is extended (Galois' Propositions II-IV).

Some recent texts on Galois theory place mistaken emphasis on the question of finding explicit quintic equations, with rational coefficients, which cannot be solved by radicals. This is a moderately interesting result (one not covered in this book) but it is not a key theorem of Galois theory. Galois showed that an algebraic equation is solvable by radicals if and only if the associated group is solvable. A given quintic with rational coefficients can therefore be tested for solvability. Abel's theorem that the general quintic is not solvable states that the equation $x^5+B x^4+C x^3+D x^2+$ $E x+F=0$-an equation with coefficients in the field $\mathbb{Q}(B, C, D, E, F)$ obtained by adjoining five transcendental elements (variables) to $\mathbb{Q}$-is not solvable by radicals. (In Galois theory this follows from the fact that the Galois group of this equation is the full group of 120 permutations of the five roots.) In other words, no field extension of $\mathbb{Q}(B, C, D, E, F)$ obtained by a succession of adjunctions of radicals can ever contain a root of the given equation. This is what it means to say that the quadratic formula

$$
x=\frac{-B \pm \sqrt{B^2-4 C}}{2},
$$

and the much more complicated formulas for the cubic and quartic equations (Exercises 1 and 2 of the Sixth Set) have no generalization to the quintic equation.


### Newton and Symmetric Functions

§8 [[Isaac Newton]] (1643-1727) is most famous for his discovery of the universal law of gravitation and for his use of that law to give an exact mathematical description of planetary motion. Consequently, he is identified in most people's minds with mathematical physics and applied mathematics. Even people who have some acquaintance with the history of mathematics and who realize that Newton, with Leibniz, is regarded as the father of differential and integral calculus, tend to think of Newton's mathematics as being closely related to his physics, and his calculus as being primarily a tool in his study of motion. Nevertheless, Newton's contributions to pure mathematics alone are sufficient to place him among the greatest geniuses in the history of mathematics. This section is devoted to a theorem of pure algebra which is of crucial importance to the later development of the subject and which appears to be Newton's creation.

A portion of this theorem was published in Newton's Arithmetica Universalis in 1707, after Newton was world famous and had ceased active scientific work. It is cited by Gauss [G2, Art. 338] and Weber [W3, vol. I, Sec. 46], among others, and is generally known as Newton's theorem. Of course the Arithmetica Universalis was known to have been written long before 1707, but it is only with the recent work of Derek T. Whiteside in analyzing, annotating, and publishing Newton's notebooks and papers that it has been possible to date many of Newton's discoveries and, in the case of the theorem under discussion, to know that he was aware at a very early date of the full theorem, not just the portion given in the Arithmetica Universalis.
§9 Whiteside found in papers dating to 1665-1666, in the very earliest phase of Newton's career, the following formulas: Let $r, s, t$ be the three roots of a cubic equation $x^3+b x^2+c x+d=0$, and let an expression like "every $r^i s^j$ " denote the sum of all distinct expressions of the form $r^i s^j$ where $r$ and $s$ are roots of the given cubic, i.e. "every $r^2 s$ " $=r^2 s+s^2 t+t^2 r+r^2 t+$ $t^2 s+s^2 r$, "every $r^2 "=r^2+s^2+t^2$, "every $r^2 s^2 t^2 "=r^2 s^2 t^2$, etc. Then Newton's formulas* are

$$
\begin{aligned}
(\text { every } r) & =-b \\
(\text { every } r^2) & =b^2-2 c \\
\left(\text { every } r^3\right) & =-b^3+3 b c-3 d \\
(\text { every } r s) & =c \\
(\text { every } r^2 s) & =-b c+3 d \\
\left(\text { every } r^3 s\right) & =b^2 c-2 c^2-b d \\
\left(\text { every } r^2 s^2\right) & =c^2-2 b d \\
\left(\text { every } r^3 s^2\right) & =-b c^2+2 b^2 d+c d \\
\left(\text { every } r^3 s^3\right) & =c^3-3 b c d+3 d^2 \\
\left(\text { every } r s t\right) & =-d \\
\left(\text { every } r^2 s t\right) & =b d \\
\left(\text { every } r^3 s t\right) & =-b^2 d+2 c d \\
\left(\text { every } r^2 s^2 t\right) & =-c d \\
\left(\text { every } r^3 s^2 t\right) & =b c d-3 d^2 \\
\left(\text { every } r^3 s^3 t\right) & =-c^2 d+2 b d^2 \\
\left(\text { every } r^2 s^2 t^2\right) & =d^2 \\
\left(\text { every } r^3 s^2 t^2\right) & =-b d^2 \\
\left(\text { every } r^3 s^3 t^2\right) & =c d^2 \\
\left(\text { every } r^3 s^3 t^3\right) & =-d^3
\end{aligned}
$$
$$
\begin{aligned}

\end{aligned}
$$

He did not record in his notes the method by which he derived these formulas, and we can only guess what lay behind them. However, it seems likely that the choice to stop with third powers of the roots was arbitrary* and that he could have given analogous formulas for higher powers. Moreover, the decision to deal with the three roots of a cubic, rather than the four roots of a quartic or the five roots of a quintic, was also probably arbitrary. In fact, a few pages later in Whiteside's book, a passage from Newton's notebook is reproduced in which he gives the analogs of formulas (1)-(3) for an equation of degree 8 , namely, the formulas $\dagger$

$$
\begin{aligned}
(\text { every } r)= & -p \\
\left(\text { every } r^2\right)= & p^2-2 q \\
\left(\text { every } r^3\right)= & -p^3+3 p q-3 r \\
\left(\text { every } r^4\right)= & p^4-4 p^2 q+4 p r-4 s+2 q^2 \\
\left(\text { every } r^5\right)= & -p^5+5 p^3 q-5 p^2 r+5 p s-5 t-5 p q^2+5 q r \\
\left(\text { every } r^6\right)= & p^6-6 p^4 q+6 p^3 r-6 p^2 s+6 p t-6 v+9 p^2 q^2 \\
& -12 p q r+6 q s-2 q^3 \\
\left(\text { every } r^7\right)= & -p^7+7 p^5 q-7 p^4 r+7 p^3 s-7 p^2 t+7 p v-7 y \\
\left(\text { every } r^8\right)= & p^8-8 p^6 q+8 p^5 r-8 p^4 s+8 p^3 t-8 p^2 v+8 p y-8 z
\end{aligned}
$$

### The Fundamental Theorem on Symmetric Polynomials

§10 The first step in giving a careful statement of the theorem is to remove the reference to roots of an $n$th degree equation, because these roots may be irrational or complex and they are really extraneous to the theorem. (Newton explicitly states in his formulas that the roots may be "false", i.e. negative, or "imaginary".) The particular formulas (1), (4) and (10) in Newton's list, that is,

$$
\begin{aligned}
r+s+t & =-b \\
r s+s t+t r & =c \\
r s t & =-d
\end{aligned}
$$

are especially important and were probably rather widely known in Newton's time. (Whiteside [N3, p. 518, note 12] observes that the general case of these formulas was published by Albert Girard in 1629 but says that "we may assume" that Newton's version of it, which he published in the Arithmetica Universalis, was his "independent discovery".) These formulas follow immediately from the identity

$$
x^3+b x^2+c x+d=(x-r)(x-s)(x-t),
$$

when the right side is multiplied out and coefficients of like powers of $x$ are equated. The same procedure applied to

$$
x^n+b_1 x^{n-1}+b_2 x^{n-2}+\cdots+b_n=\left(x-r_1\right)\left(x-r_2\right) \cdots\left(x-r_n\right)
$$

shows that, in analogy to (20), the sum of all* $\binom{n}{k}$ products of $k$ of the $r_i$ is equal to $(-1)^k b_k$. That is,

$$
\begin{aligned}
r_1+r_2+\cdots+r_n & =-b_1 \\
r_1 r_2+r_1 r_3+\cdots+r_{n-1} r_n & =b_2 \\
r_1 r_2 r_3+r_1 r_2 r_4+\cdots+r_{n-2} r_{n-1} r_n & =-b_3 \\
& \vdots \\
r_1 r_2 \cdots r_n & =(-1)^n b_n
\end{aligned}
$$

Let $\sigma_k$ denote the polynomial on the left side of the $k$ th equation, so that the equation reads $\sigma_k=(-1)^k b_k$. Then $\sigma_k$ is called the $k$ th elementary symmetric polynomial in $r_1, r_2, \ldots, r_n$. Here $r_1, r_2, \ldots, r_n$ are to be regarded as variables or indeterminates, rather than roots of an equation, and $\sigma_1, \sigma_2, \ldots, \sigma_n$ are to be regarded as polynomials in these indeterminates. A polynomial in $r_1, r_2, \ldots, r_n$ is simply a formal sum of terms of the form $A r_1^{\mu_1} r_2^{\mu_2} \cdots r_n^{\mu_n}$ where $A$ is a number (say a rational number for now) and the $\mu$ 's are nonnegative integers. A polynomial in $r_1, r_2, \ldots, r_n$ is said to be symmetric if it has the property that interchanging any two of the $r$ 's leaves the polynomial un-changed-provided, of course, that two polynomials are regarded as being equal when applications of the commutative laws of addition and multiplication can change one into the other. (For example, $r s+s t+t r$ is unchanged by an interchange of $r$ and $s$ because $r s+s t+t r=s r+r t+t s$.) Clearly the elementary symmetric polynomials $\sigma_1, \sigma_2, \ldots, \sigma_n$ in $n$ variables are symmetric in this definition.

In Newton's formulas (1)-(19) the left sides are by definition symmetric in $r, s$, and $t$, and the right sides are polynomials in $b, c$, and $d$ or, what is the same in view of (20), polynomials in $\sigma_1=r+s+t, \sigma_2=r s+s t+t r$, and $\sigma_3=r s t$. Thus these formulas are all instances of the following theorem:

**Fundamental Theorem on Symmetric Polynomials.** Every symmetric polynomial in $r_1, r_2, \ldots, r_n$ can be expressed as a polynomial in the elementary symmetric polynomials $\sigma_1, \sigma_2, \ldots, \sigma_n$. Moreover, a symmetric polynomial with integer coefficients can be expressed as a polynomial in $\sigma_1, \sigma_2, \ldots, \sigma_n$ with integer coefficients.

When the theorem is stated in this way, it deals with algebraic identities, not with equations and roots. For example, Newton's formula (3) is the identity

$$
\begin{aligned}
r^3+s^3+t^3 & =\sigma_1^3-3 \sigma_1 \sigma_2+3 \sigma_3 \\
& =(r+s+t)^3-3(r+s+t)(r s+s t+t r)+3 r s t
\end{aligned}
$$


However, if $x^n+b_1 x^{n-1}+b_2 x^{n-2}+\cdots+b_n=0$ is an $n$th degree equation with $n$ roots (in some sense) the formula $\sigma_k=(-1)^k b_k$ makes it possible to evaluate the elementary symmetric functions of the roots immediately, without ever finding the roots themselves; then the theorem shows that it is possible to evaluate any symmetric function of the roots without finding the roots themselves. Moreover-a fact that will be very important later on-if the $b$ 's are rational numbers, then any symmetric polynomial in the roots assumes a rational value.