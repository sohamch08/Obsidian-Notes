---
tag: integral-dependence
---
The meaning of 'an element $x$ in $B$ integral over $A$' is explained in [[Integral Dependence]]

>[!def] Definition (Integral Closure)
>The set of elements of $B$ which are integral over $A$ is called the integral closure

- If $C=A$ then $A$ is called integrally closed in $B$
- If $C=B$ the ring $B$ is said to be integral over $A$ 

> [!thm]
> Integral Closure is a subring of $B$ containing $A$

For the proof it uses the corollary that if $x_1,\dots,x_n$ are integral over $A$ then $A[x_1,\dots,x_n]$ is finitely generated $A-module$ in [[Integral Dependence]] 

> [!cor] 
> Let $A\subseteq B$ be rings and let $C$ be the integral closure of $A$ in $B$. Then $C$ is [[Integrally Closed]] in $B$

>[!prop]
>Let $A\subeq B$ be rings, $C$ be the Integral closure of $A$ in $B$. Let $S$ be a multiplicatively closed subset of $A$ . Then $S^{-1}C$ is the integral closure of $S^{-1}A$

> Integral closure is a [[Local Property]]

>[!thm] 
>Let $A$ be an [[Integral Domain]]. Then the following are equivalent:
>1. $A$ is [[Integrally Closed]]
>2. $A_{\mfp}$ is integrally closed, for each [[Prime Ideal]] $\mfp$
>3. $A_{\mfm}$ is integrally  closed, for each [[Maximal Ideal]] $\mfm$
