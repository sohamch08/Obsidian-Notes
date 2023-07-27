---
tag: tree
---
>[!definition] Definition (Trees)
>A tree is a [[Connected]] [[Acyclic]] [[Graph]]
>- A **Leaf** is a vertex of degree 1


- Paths are trees. A tree is a path $\iff$ its maximum degree is 2

## Basic Properties

>[!lemma] 
>- Every tree with at least two vertices has at least two leaves.
>- Deleting a leaf from an $n-$vertex produces a tree with $n-1$ vertices

***Proof:*** 
- A [[Connected]] graph with at least two vertices has an edge. In an [[Acyclic]] graph an endpoint of a maximal nontrivial path has no neighbor other than its neighbor on the path. Hence the endpoints of a such a path are leaves. $\blacksquare$
- Let $v$ be a leaf of a tree $G$ and let $G'=G-v$. A vertex of degree 1 belongs to no path connecting two other vertices. Therefore for $u,w\in V(G')$ every every path $u,w-$path in $G$ is also in $G'$. Hence $G'$ is connected. Since deleting a vertex cannot create a [[Cycle]], $G'$ is also [[Acyclic]]. Thus $G'$ is a tree with $n-1$ vertices. $\blacksquare$

>[!theorem] 
>For an $n-$vertex graph $G$ (with $n\geq1$) the following are equivalent ( and characterize the trees with $n$ vertices)
>1. $G$ is [[Connected]] and has no [[Cycle]]s
>2. $G$ is [[Connected]] and has $n-1$ edges 
>3. $G$ has $n-1$ edges and no [[Cycle]]s
>4. $G$ has no loops and has for each $u,v\in V(G)$ exactly one $u,v$ path

***Proof:*** We first demonstrate the equivalence of (1), (2) and (3) by proving that any two of ([[Connected]], [[Acyclic]], $n-1$ edges) together imply the third
1. $(1)\implies \{(2),(3)\}:$ We use induction on $n$.  For $n=1$ an acyclic $1-$vertex graph has no edge. For $n>1$ er suppose that the implication holds for graphs with fewer than $n$ vertices. Given an [[Acyclic]] [[Connected]] graph $G$. By the previous lemma we have a leaf $v$ and states that $G'=G-v$ also is acyclic and connected. Applying the induction hypothesis to $G'$ yields $r(G')=n-2$. Since only one edge is incident to $v$, we have $e(G)=n-1$.
2. $(2)\implies \{(1),(3)\}:$ Delete edges from [[Cycle]]s of $G$ one by one until the resulting graph $G'$ is [[Acyclic]]. Since no edge of a cycle is a [[Cut Edge]] (Last Theorem). $G'$ is [[Connected]]. Now the part (1) implies that $e(G')=n-1$. Since we are given $e(G)=n-1$ no edges were deleted. Thus $G=G'$. and $G$ is acyclic.
3. $(1)\implies \{(1),(2)\}:$ Let $G_1,\dots,G_k$ be the [[Components]] of $G$. Since $G$ has no [[Cycle]]s each component has no cycles. So $e(G_i)=n(G_i)-1$. So $$e(G)=\sum_{i=1}^k [n(G_i)-1]=n-k$$ We are given $e(G)=n-1$. So $k=1$. Hence $G$ is [[Connected]].
4. $(1)\implies (4):$ Since $G$ is [[Connected]], each pair of vertices is connected by a path. If some pair is connected by more than one, we choose a shortest pair $P,Q$ of distinct paths with the same endpoints. If $P,Q$ share a common internal vertex, we take the first common vertex suppose $w$ then we have two distinct path joining $u,w$ with the paths have no common internal vertex. So the union of the paths creates a [[Cycle]] which contradicts the hypothesis.
5. $(4)\implies (1):$ For each $u,v\in V(G)$ there is a $u,v-$path. Hence $G$ is [[Connected]]. If $G$ has a cycle then $G$ has two $u,v-$paths for $u,v\in V(G)$. Hence $G$ is [[Acyclic]]. $\blacksquare$


>[!corollary] 
>1. Every edge of a tree is a [[Cut Edge]]
>2. Adding one edge to a tree forms exactly one [[Cycle]]
>3. Every [[Connected]] graph contains a [[Spanning Tree]]

***Proof:*** 
1. A tree has no cycles, so by last theorem of [[Cut Edge]] every edge is a cut edge.
2. A tree has a unique path linking each pair of vertices. So joining two vertices with an edge creates exactly one cycle
3. As in the proof of $(2)\implies \{(1),(3)\}$ in previous theorem iteratively deleting edges from cycles in a [[Connected]] graph yields a connected [[Acyclic]] [[Spanning Subgraph]]. $\blacksquare$

>[!proposition] 
>If $T$ is a tree with $k$ edges and $G$ is a simple graph with $\delta(G)\geq k$ then $T$ is a [[Subgraph]] of $G$

***Proof:*** We use induction on $k$. 
For $k=0$ every simple graph contain $K_1$ ([[Complete]]) which is the only tree with no edges.
Induction Step: $k>0$ We assume that the claim holds for trees with fewer than $k$ edges.
Since $k>0$ the first lemma allows us to choose a leaf $v$ in $T$. Let $u$ be its neighbor. Consider the smaller tree $T'=T-v$. By the induction hypothesis $G$ contains $T'$ as a subgraph since $\delta(G)\geq k>k-1$.
Let $x$ be the vertex in this copy of $T'$ that corresponds to $u$. Because $T'$ has only $k-1$ vertices other than $u$ and $d_G(x)\geq k$, $x$ has a neighbor $y$ in $G$ that is not in this copy $T'$. Adding the edge $xy$ expands this copy of $T'$ into a copy of $T$ in $G$ with $y$ playing the role of $v$. $\blacksquare$







































$$%---------------------------------------
% BlackBoard Math Fonts :-
%---------------------------------------

%Captital Letters
\newcommand{\bbA}{\mathbb{A}}	\newcommand{\bbB}{\mathbb{B}}
\newcommand{\bbC}{\mathbb{C}}	\newcommand{\bbD}{\mathbb{D}}
\newcommand{\bbE}{\mathbb{E}}	\newcommand{\bbF}{\mathbb{F}}
\newcommand{\bbG}{\mathbb{G}}	\newcommand{\bbH}{\mathbb{H}}
\newcommand{\bbI}{\mathbb{I}}	\newcommand{\bbJ}{\mathbb{J}}
\newcommand{\bbK}{\mathbb{K}}	\newcommand{\bbL}{\mathbb{L}}
\newcommand{\bbM}{\mathbb{M}}	\newcommand{\bbN}{\mathbb{N}}
\newcommand{\bbO}{\mathbb{O}}	\newcommand{\bbP}{\mathbb{P}}
\newcommand{\bbQ}{\mathbb{Q}}	\newcommand{\bbR}{\mathbb{R}}
\newcommand{\bbS}{\mathbb{S}}	\newcommand{\bbT}{\mathbb{T}}
\newcommand{\bbU}{\mathbb{U}}	\newcommand{\bbV}{\mathbb{V}}
\newcommand{\bbW}{\mathbb{W}}	\newcommand{\bbX}{\mathbb{X}}
\newcommand{\bbY}{\mathbb{Y}}	\newcommand{\bbZ}{\mathbb{Z}}

%---------------------------------------
% MathCal Fonts :-
%---------------------------------------

%Captital Letters
\newcommand{\mcA}{\mathcal{A}}	\newcommand{\mcB}{\mathcal{B}}
\newcommand{\mcC}{\mathcal{C}}	\newcommand{\mcD}{\mathcal{D}}
\newcommand{\mcE}{\mathcal{E}}	\newcommand{\mcF}{\mathcal{F}}
\newcommand{\mcG}{\mathcal{G}}	\newcommand{\mcH}{\mathcal{H}}
\newcommand{\mcI}{\mathcal{I}}	\newcommand{\mcJ}{\mathcal{J}}
\newcommand{\mcK}{\mathcal{K}}	\newcommand{\mcL}{\mathcal{L}}
\newcommand{\mcM}{\mathcal{M}}	\newcommand{\mcN}{\mathcal{N}}
\newcommand{\mcO}{\mathcal{O}}	\newcommand{\mcP}{\mathcal{P}}
\newcommand{\mcQ}{\mathcal{Q}}	\newcommand{\mcR}{\mathcal{R}}
\newcommand{\mcS}{\mathcal{S}}	\newcommand{\mcT}{\mathcal{T}}
\newcommand{\mcU}{\mathcal{U}}	\newcommand{\mcV}{\mathcal{V}}
\newcommand{\mcW}{\mathcal{W}}	\newcommand{\mcX}{\mathcal{X}}
\newcommand{\mcY}{\mathcal{Y}}	\newcommand{\mcZ}{\mathcal{Z}}



%---------------------------------------
% Bold Math Fonts :-
%---------------------------------------

%Captital Letters
\newcommand{\bmA}{\boldsymbol{A}}	\newcommand{\bmB}{\boldsymbol{B}}
\newcommand{\bmC}{\boldsymbol{C}}	\newcommand{\bmD}{\boldsymbol{D}}
\newcommand{\bmE}{\boldsymbol{E}}	\newcommand{\bmF}{\boldsymbol{F}}
\newcommand{\bmG}{\boldsymbol{G}}	\newcommand{\bmH}{\boldsymbol{H}}
\newcommand{\bmI}{\boldsymbol{I}}	\newcommand{\bmJ}{\boldsymbol{J}}
\newcommand{\bmK}{\boldsymbol{K}}	\newcommand{\bmL}{\boldsymbol{L}}
\newcommand{\bmM}{\boldsymbol{M}}	\newcommand{\bmN}{\boldsymbol{N}}
\newcommand{\bmO}{\boldsymbol{O}}	\newcommand{\bmP}{\boldsymbol{P}}
\newcommand{\bmQ}{\boldsymbol{Q}}	\newcommand{\bmR}{\boldsymbol{R}}
\newcommand{\bmS}{\boldsymbol{S}}	\newcommand{\bmT}{\boldsymbol{T}}
\newcommand{\bmU}{\boldsymbol{U}}	\newcommand{\bmV}{\boldsymbol{V}}
\newcommand{\bmW}{\boldsymbol{W}}	\newcommand{\bmX}{\boldsymbol{X}}
\newcommand{\bmY}{\boldsymbol{Y}}	\newcommand{\bmZ}{\boldsymbol{Z}}
%Small Letters
\newcommand{\bma}{\boldsymbol{a}}	\newcommand{\bmb}{\boldsymbol{b}}
\newcommand{\bmc}{\boldsymbol{c}}	\newcommand{\bmd}{\boldsymbol{d}}
\newcommand{\bme}{\boldsymbol{e}}	\newcommand{\bmf}{\boldsymbol{f}}
\newcommand{\bmg}{\boldsymbol{g}}	\newcommand{\bmh}{\boldsymbol{h}}
\newcommand{\bmi}{\boldsymbol{i}}	\newcommand{\bmj}{\boldsymbol{j}}
\newcommand{\bmk}{\boldsymbol{k}}	\newcommand{\bml}{\boldsymbol{l}}
\newcommand{\bmm}{\boldsymbol{m}}	\newcommand{\bmn}{\boldsymbol{n}}
\newcommand{\bmo}{\boldsymbol{o}}	\newcommand{\bmp}{\boldsymbol{p}}
\newcommand{\bmq}{\boldsymbol{q}}	\newcommand{\bmr}{\boldsymbol{r}}
\newcommand{\bms}{\boldsymbol{s}}	\newcommand{\bmt}{\boldsymbol{t}}
\newcommand{\bmu}{\boldsymbol{u}}	\newcommand{\bmv}{\boldsymbol{v}}
\newcommand{\bmw}{\boldsymbol{w}}	\newcommand{\bmx}{\boldsymbol{x}}
\newcommand{\bmy}{\boldsymbol{y}}	\newcommand{\bmz}{\boldsymbol{z}}

%---------------------------------------
% Scr Math Fonts :-
%---------------------------------------

\newcommand{\sA}{{\mathscr{A}}}   \newcommand{\sB}{{\mathscr{B}}}
\newcommand{\sC}{{\mathscr{C}}}   \newcommand{\sD}{{\mathscr{D}}}
\newcommand{\sE}{{\mathscr{E}}}   \newcommand{\sF}{{\mathscr{F}}}
\newcommand{\sG}{{\mathscr{G}}}   \newcommand{\sH}{{\mathscr{H}}}
\newcommand{\sI}{{\mathscr{I}}}   \newcommand{\sJ}{{\mathscr{J}}}
\newcommand{\sK}{{\mathscr{K}}}   \newcommand{\sL}{{\mathscr{L}}}
\newcommand{\sM}{{\mathscr{M}}}   \newcommand{\sN}{{\mathscr{N}}}
\newcommand{\sO}{{\mathscr{O}}}   \newcommand{\sP}{{\mathscr{P}}}
\newcommand{\sQ}{{\mathscr{Q}}}   \newcommand{\sR}{{\mathscr{R}}}
\newcommand{\sS}{{\mathscr{S}}}   \newcommand{\sT}{{\mathscr{T}}}
\newcommand{\sU}{{\mathscr{U}}}   \newcommand{\sV}{{\mathscr{V}}}
\newcommand{\sW}{{\mathscr{W}}}   \newcommand{\sX}{{\mathscr{X}}}
\newcommand{\sY}{{\mathscr{Y}}}   \newcommand{\sZ}{{\mathscr{Z}}}


%---------------------------------------
% Math Fraktur Font
%---------------------------------------

%Captital Letters
\newcommand{\mfA}{\mathfrak{A}}	\newcommand{\mfB}{\mathfrak{B}}
\newcommand{\mfC}{\mathfrak{C}}	\newcommand{\mfD}{\mathfrak{D}}
\newcommand{\mfE}{\mathfrak{E}}	\newcommand{\mfF}{\mathfrak{F}}
\newcommand{\mfG}{\mathfrak{G}}	\newcommand{\mfH}{\mathfrak{H}}
\newcommand{\mfI}{\mathfrak{I}}	\newcommand{\mfJ}{\mathfrak{J}}
\newcommand{\mfK}{\mathfrak{K}}	\newcommand{\mfL}{\mathfrak{L}}
\newcommand{\mfM}{\mathfrak{M}}	\newcommand{\mfN}{\mathfrak{N}}
\newcommand{\mfO}{\mathfrak{O}}	\newcommand{\mfP}{\mathfrak{P}}
\newcommand{\mfQ}{\mathfrak{Q}}	\newcommand{\mfR}{\mathfrak{R}}
\newcommand{\mfS}{\mathfrak{S}}	\newcommand{\mfT}{\mathfrak{T}}
\newcommand{\mfU}{\mathfrak{U}}	\newcommand{\mfV}{\mathfrak{V}}
\newcommand{\mfW}{\mathfrak{W}}	\newcommand{\mfX}{\mathfrak{X}}
\newcommand{\mfY}{\mathfrak{Y}}	\newcommand{\mfZ}{\mathfrak{Z}}
%Small Letters
\newcommand{\mfa}{\mathfrak{a}}	\newcommand{\mfb}{\mathfrak{b}}
\newcommand{\mfc}{\mathfrak{c}}	\newcommand{\mfd}{\mathfrak{d}}
\newcommand{\mfe}{\mathfrak{e}}	\newcommand{\mff}{\mathfrak{f}}
\newcommand{\mfg}{\mathfrak{g}}	\newcommand{\mfh}{\mathfrak{h}}
\newcommand{\mfi}{\mathfrak{i}}	\newcommand{\mfj}{\mathfrak{j}}
\newcommand{\mfk}{\mathfrak{k}}	\newcommand{\mfl}{\mathfrak{l}}
\newcommand{\mfm}{\mathfrak{m}}	\newcommand{\mfn}{\mathfrak{n}}
\newcommand{\mfo}{\mathfrak{o}}	\newcommand{\mfp}{\mathfrak{p}}
\newcommand{\mfq}{\mathfrak{q}}	\newcommand{\mfr}{\mathfrak{r}}
\newcommand{\mfs}{\mathfrak{s}}	\newcommand{\mft}{\mathfrak{t}}
\newcommand{\mfu}{\mathfrak{u}}	\newcommand{\mfv}{\mathfrak{v}}
\newcommand{\mfw}{\mathfrak{w}}	\newcommand{\mfx}{\mathfrak{x}}
\newcommand{\mfy}{\mathfrak{y}}	\newcommand{\mfz}{\mathfrak{z}}

%---------------------------------------
% Bar
%---------------------------------------

%Captital Letters
\newcommand{\ovA}{\overline{A}}	\newcommand{\ovB}{\overline{B}}
\newcommand{\ovC}{\overline{C}}	\newcommand{\ovD}{\overline{D}}
\newcommand{\ovE}{\overline{E}}	\newcommand{\ovF}{\overline{F}}
\newcommand{\ovG}{\overline{G}}	\newcommand{\ovH}{\overline{H}}
\newcommand{\ovI}{\overline{I}}	\newcommand{\ovJ}{\overline{J}}
\newcommand{\ovK}{\overline{K}}	\newcommand{\ovL}{\overline{L}}
\newcommand{\ovM}{\overline{M}}	\newcommand{\ovN}{\overline{N}}
\newcommand{\ovO}{\overline{O}}	\newcommand{\ovP}{\overline{P}}
\newcommand{\ovQ}{\overline{Q}}	\newcommand{\ovR}{\overline{R}}
\newcommand{\ovS}{\overline{S}}	\newcommand{\ovT}{\overline{T}}
\newcommand{\ovU}{\overline{U}}	\newcommand{\ovV}{\overline{V}}
\newcommand{\ovW}{\overline{W}}	\newcommand{\ovX}{\overline{X}}
\newcommand{\ovY}{\overline{Y}}	\newcommand{\ovZ}{\overline{Z}}
%Small Letters
\newcommand{\ova}{\overline{a}}	\newcommand{\ovb}{\overline{b}}
\newcommand{\ovc}{\overline{c}}	\newcommand{\ovd}{\overline{d}}
\newcommand{\ove}{\overline{e}}	\newcommand{\ovf}{\overline{f}}
\newcommand{\ovg}{\overline{g}}	\newcommand{\ovh}{\overline{h}}
\newcommand{\ovi}{\overline{i}}	\newcommand{\ovj}{\overline{j}}
\newcommand{\ovk}{\overline{k}}	\newcommand{\ovl}{\overline{l}}
\newcommand{\ovm}{\overline{m}}	\newcommand{\ovn}{\overline{n}}
\newcommand{\ovo}{\overline{o}}	\newcommand{\ovp}{\overline{p}}
\newcommand{\ovq}{\overline{q}}	\newcommand{\ovr}{\overline{r}}
\newcommand{\ovs}{\overline{s}}	\newcommand{\ovt}{\overline{t}}
\newcommand{\ovu}{\overline{u}}	\newcommand{\ovv}{\overline{v}}
\newcommand{\ovw}{\overline{w}}	\newcommand{\ovx}{\overline{x}}
\newcommand{\ovy}{\overline{y}}	\newcommand{\ovz}{\overline{z}}

%---------------------------------------
% Tilde
%---------------------------------------

%Captital Letters
\newcommand{\tdA}{\tilde{A}}	\newcommand{\tdB}{\tilde{B}}
\newcommand{\tdC}{\tilde{C}}	\newcommand{\tdD}{\tilde{D}}
\newcommand{\tdE}{\tilde{E}}	\newcommand{\tdF}{\tilde{F}}
\newcommand{\tdG}{\tilde{G}}	\newcommand{\tdH}{\tilde{H}}
\newcommand{\tdI}{\tilde{I}}	\newcommand{\tdJ}{\tilde{J}}
\newcommand{\tdK}{\tilde{K}}	\newcommand{\tdL}{\tilde{L}}
\newcommand{\tdM}{\tilde{M}}	\newcommand{\tdN}{\tilde{N}}
\newcommand{\tdO}{\tilde{O}}	\newcommand{\tdP}{\tilde{P}}
\newcommand{\tdQ}{\tilde{Q}}	\newcommand{\tdR}{\tilde{R}}
\newcommand{\tdS}{\tilde{S}}	\newcommand{\tdT}{\tilde{T}}
\newcommand{\tdU}{\tilde{U}}	\newcommand{\tdV}{\tilde{V}}
\newcommand{\tdW}{\tilde{W}}	\newcommand{\tdX}{\tilde{X}}
\newcommand{\tdY}{\tilde{Y}}	\newcommand{\tdZ}{\tilde{Z}}
%Small Letters
\newcommand{\tda}{\tilde{a}}	\newcommand{\tdb}{\tilde{b}}
\newcommand{\tdc}{\tilde{c}}	\newcommand{\tdd}{\tilde{d}}
\newcommand{\tde}{\tilde{e}}	\newcommand{\tdf}{\tilde{f}}
\newcommand{\tdg}{\tilde{g}}	\newcommand{\tdh}{\tilde{h}}
\newcommand{\tdi}{\tilde{i}}	\newcommand{\tdj}{\tilde{j}}
\newcommand{\tdk}{\tilde{k}}	\newcommand{\tdl}{\tilde{l}}
\newcommand{\tdm}{\tilde{m}}	\newcommand{\tdn}{\tilde{n}}
\newcommand{\tdo}{\tilde{o}}	\newcommand{\tdp}{\tilde{p}}
\newcommand{\tdq}{\tilde{q}}	\newcommand{\tdr}{\tilde{r}}
\newcommand{\tds}{\tilde{s}}	\newcommand{\tdt}{\tilde{t}}
\newcommand{\tdu}{\tilde{u}}	\newcommand{\tdv}{\tilde{v}}
\newcommand{\tdw}{\tilde{w}}	\newcommand{\tdx}{\tilde{x}}
\newcommand{\tdy}{\tilde{y}}	\newcommand{\tdz}{\tilde{z}}

%---------------------------------------
% Vec
%---------------------------------------

%Captital Letters
\newcommand{\vA}{\vec{A}}	\newcommand{\vB}{\vec{B}}
\newcommand{\vC}{\vec{C}}	\newcommand{\vD}{\vec{D}}
\newcommand{\vE}{\vec{E}}	\newcommand{\vF}{\vec{F}}
\newcommand{\vG}{\vec{G}}	\newcommand{\vH}{\vec{H}}
\newcommand{\vI}{\vec{I}}	\newcommand{\vJ}{\vec{J}}
\newcommand{\vK}{\vec{K}}	\newcommand{\vL}{\vec{L}}
\newcommand{\vM}{\vec{M}}	\newcommand{\vN}{\vec{N}}
\newcommand{\vO}{\vec{O}}	\newcommand{\vP}{\vec{P}}
\newcommand{\vQ}{\vec{Q}}	\newcommand{\vR}{\vec{R}}
\newcommand{\vS}{\vec{S}}	\newcommand{\vT}{\vec{T}}
\newcommand{\vU}{\vec{U}}	\newcommand{\vV}{\vec{V}}
\newcommand{\vW}{\vec{W}}	\newcommand{\vX}{\vec{X}}
\newcommand{\vY}{\vec{Y}}	\newcommand{\vZ}{\vec{Z}}
%Small Letters
\newcommand{\va}{\vec{a}}	\newcommand{\vb}{\vec{b}}
\newcommand{\vc}{\vec{c}}	\newcommand{\vd}{\vec{d}}
\newcommand{\ve}{\vec{e}}	\newcommand{\vf}{\vec{f}}
\newcommand{\vg}{\vec{g}}	\newcommand{\vh}{\vec{h}}
\newcommand{\vi}{\vec{i}}	\newcommand{\vj}{\vec{j}}
\newcommand{\vk}{\vec{k}}	\newcommand{\vl}{\vec{l}}
\newcommand{\vm}{\vec{m}}	\newcommand{\vn}{\vec{n}}
\newcommand{\vo}{\vec{o}}	\newcommand{\vp}{\vec{p}}
\newcommand{\vq}{\vec{q}}	\newcommand{\vr}{\vec{r}}
\newcommand{\vs}{\vec{s}}	\newcommand{\vt}{\vec{t}}
\newcommand{\vu}{\vec{u}}	\newcommand{\vv}{\vec{v}}
\newcommand{\vw}{\vec{w}}	\newcommand{\vx}{\vec{x}}
\newcommand{\vy}{\vec{y}}	\newcommand{\vz}{\vec{z}}

%---------------------------------------
% Greek Letters:-
%---------------------------------------
\newcommand{\eps}{\epsilon}
\newcommand{\veps}{\varepsilon}
\newcommand{\lm}{\lambda}
\newcommand{\Lm}{\Lambda}
\newcommand{\gm}{\gamma}
\newcommand{\Gm}{\Gamma}
\newcommand{\vph}{\varphi}
\newcommand{\ph}{\phi}
\newcommand{\om}{\omega}
\newcommand{\Om}{\Omega}
\newcommand{\Qed}{\begin{flushright}\qed\end{flushright}}
\newcommand{\del}[2]{\frac{\partial #1}{\partial #2}}
\newcommand{\Del}[3]{\frac{\partial^{#1} #2}{\partial^{#1} #3}}
\newcommand{\deld}[2]{\dfrac{\partial #1}{\partial #2}}
\newcommand{\Deld}[3]{\dfrac{\partial^{#1} #2}{\partial^{#1} #3}}
\newcommand{\uin}{\mathbin{\rotatebox[origin=c]{90}{$\in$}}}
\newcommand{\usubset}{\mathbin{\rotatebox[origin=c]{90}{$\subset$}}}
\newcommand{\lt}{\left}
\newcommand{\rt}{\right}
\newcommand{\exs}{\exists}
\newcommand{\st}{\strut}
\newcommand{\dps}[1]{\displaystyle{#1}}
\newcommand{\mat}[1]{\left[\begin{matrix}#1\end{matrix}\right]}
\newcommand{\subeq}{\subseteq}
\newcommand{\qed}{\blacksquare}

$$