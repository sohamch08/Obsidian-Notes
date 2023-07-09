$$
\newcommand{\l}{\lambda}
\newcommand{\L}{\Lambda}
\newcommand{\ra}{\rightarrow}
\newcommand{\rab}{\rightarrow_\beta}
\newcommand{\fk}[1]{\mathfrak{#1}}
\newcommand{\fv}{\fk{fv}}
\newcommand{\bv}{\fk{bv}}
\newcommand{\ns}{\emptyset}
\newcommand{\N}{\mathbb{N}}
$$

# $\l$-Calculus
Assume a countably infinite set $Var$ of variables. The set $\Lambda$ of lambda expressions is given by:
$$M := x\mid\l. M\mid MM$$ where $M$ is a term and $x\in Var$.


| Rule 1 | Rule 2 | Rule 3 |
| -------- | -------- | -------- |
| $$\frac{ }{x \in \L} x\in Var$$     | $$\frac{M \in \L,\ N\in \L }{(MN) \in \L}$$     |  $$\frac{M \in \L}{(\l x.M) \in \L}$$   |

Here $\l.M$ is called **Abstraction**, and $MN$ is called **Application**.

## Syntax rule
* Application associates to the left. $MNP \equiv ((MN)P)$
* Abstraction associates to the right
    - $\l x_1 · (\l x_2 \cdots (\l x_n · M) \cdots )$ is abbreviated $\l x_1 x_2 \cdots x_n · M$. Unless otherwise brack-
eted, the body of an abstraction is as much as possible of the rest of
the term.
    - $\l x·MN$ means $(\l x·(MN))$. Everything after the · is the body.
    - Use $(\l x·M)N$ for applying $\l x · M$ to $N$

## Free and Bound Variable
$\fk {fv}(M)$: set of all variables occurring free in $M$
* $\fv(x) = \{x\}$, for any $x \in Var$
* $\fv(MN) = \fv(M) \cup \fv(N)$
* $\fv(\l x.M) = \fv(M) \setminus \{x\}$

$\bv(M)$: set of all variables occurring bound in $M$
* $\bv(x) = \emptyset$, for any $x \in Var$
* $\bv(MN) = \bv(M) \cup \bv(N)$
* $\bv(λx · M) = \bv(M) \cup (\{x\} \cap \fv(M))$

A term $M$ is said to be closed if it has no free variables, i.e. $\fv(M) = \ns$.

## $\beta$ reduction rule/ Contraction rule

$$(\l x.M)N \rab M[x:=N] $$

**One step reduction rules..**
1. $$\frac{M \rab M'}{MN \rab M'N}$$ 
2. $$\frac{M \rab M'}{NM \rab NM'}$$ 
3. $$\frac{M \rab M'}{\l x.M \rab \l x. M}$$ 

**The following conventions to be followed:**
1. $x[x:=N] \equiv N$
2. $y[x:=N] \equiv y$ if $x \not \equiv y$
3. $MP[x:=N] \equiv (M[x:=N])(P[x:=N])$
4. $(\l x·P)[x := N] = \l x·P$
5. $(\l y·P)[x := N] = \l y·(P[x := N])$, where $y\not = x$ and $y \not \in \fv(N)$
6. $(\l y·P)[x := N] = \l z·((P[y := z])[x := N])$, where$y\not = x$, $y\in \fv(N)$, and $z$ does not occur in $P$ or $N$

An simple example would be:- $(\l zxy.yz)(yy) \rab \l xa.az(yy)$.

## Church Numerals ##
$$\begin{align}
[0] &= \l fx.x\\
[1] &= \l fx.(f x)\\
[2] &= \l fx.f(f x)\\
\vdots&\\
[n] &= \l fx.f(f\cdots(f x)\cdots) =\l fx. f^nx
\end{align}$$
Few utility functions for church numerals
$$
\begin{align}
[succ] =& \l pfx.f(p fx) \\
[plus] =& \l pqfx.p f(q fx)\\
[mult] =& \l pqf.p f(q f)\\
[plus] =& \l pq.pq\\
\end{align}
$$

## Recursive functions ##
The set of *recursive functions* is the smallest set which contains the **initial functions** and is closed with respect to **composition, primitive recursion, and minimalization**. If we exclude minimalization from this construction, we get the set of *primitive recursive functions*, all of which are total functions. Minimalization is the only operator which introduces partial functions (or, from a computational standpoint, non-termination).

###  Initial Functions ###
* Zero: Z(n) =0, $[Z]= \l n. (\l fx. x)$
* Succcesor: S(n) = n+1, $[succ] = \l mfx.f(m fx)$ 
* Projection: $\Pi_i^k(n_1,n_2,n_3, \cdots n_k) = n_i$, $[\Pi_i^k] = \l n_1n_2n_3\cdots n_k . n_i$

### Composition ###
Given $f : \N^k \ra \N$ and $g_1 , g_2 , \cdots , g_k : \N^h \ra \N$, the composition of $f$ and $g_1 , g_2 , \cdots, g^k$ ,
denoted $f \circ (g_1 , g_2 , \cdot , g_k )$, is the function
$$f \circ (g_1 , g_2 , \cdots, g_k )(n_1 , n_2 , \cdots, n_h ) =
f (g_1 (n_1 , n_2 , \cdots , n_h ), g_2 (n_1 , n_2 , \cdots , n_h ), \cdots, g_k (n_1 , n_2 ,\cdots , n_h ))$$
For example, the function $f(n) = n+2$ can be defined as the composition $f = S\circ S$ of the successor function with itself.

### Primitive recursion ###

Given $g : \N^k \ra \N$ and $h : \N^{k+2} \ra \N$, the function $f : \N^{k+1} \ra \N$ is defined by primitive
recursion from $g$ and $h$ if the following equalities hold:
$$
\begin{align}
f (0, n_1 , n_2 , \cdots , n_k ) &= g(n_1 , n_2 ,\cdots , n_k )\\
f (n+1, n_1 ,\cdots , n_k ) &= h(n, f (n, n_1 , n_2 ,\cdots , n_k ), n_1 ,\cdots , n_k )\\
\end{align}
$$
Here are some examples of primitive recursive definitions.
* The function plus(n, m) = n+m can be defined by primitive recursion from $g = \Pi_1^1$ and $h = S \circ \Pi_2^3$ . In other words,
$$
\begin{align}
&plus(0, n) = g(n)= \Pi_1^1(n)= n\\
&plus(m+1, n)  = h(m, plus(m, n), n)= S \circ \Pi_2^3(m, plus(m, n), n) = S(plus(m, n))
\end{align}
$$
* The function $times(n, m) = n \cdot m$ can be defined by primitive recursion from $g = Z$ and $h = plus \circ (\Pi_3^3 , \Pi^3_2 )$.

### $\mu$- recursion/Minimalization ###
Given $g : \N^{k+1} \ra \N$, the function $f : \N^k \ra \N$is defined by minimalization from g if
$$f (n_1 , n_2 , \cdots , n_k ) = \mu n.(g(n, n_1 , n_2 ,\cdots, n_k ) = 0)$$
where $\mu$ is the minimalization operator : $\mu n.P(n)$ returns the least natural number n such
that $P(n)$ holds. If $P(n)$ *does not hold for any $n$*, then the result is *undefined.*
In modern algorithmic notation, f can be computed by a while loop of the form
> n := 0;
> while (g(n,n1,n2,...,nk) != 0) {n := n+1};
> return n;

For example, consider the function $\log_2n$ defined as follows: $\log_2 n = k$, if $2^k = n$. If n is not
a power of $2$, $\log_2 n$ is undefined. The function $\log_2$ can be defined by minimalization from
the function $g(k, n) = 2^k − n.$


-- Created by Soham Chatterjee (sohamchatterjee999@gmail.com) and Saptarshi Sahoo  (uzumaki.sahoo@gmail.com)

