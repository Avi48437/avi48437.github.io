---
title: 'Lecture 1: Modes of Convergence'
author:
  - name: Avinandan Roy
engine: knitr
date: 2026-01-10T00:00:00.000Z
math: true
summary: >-
  Introduces almost sure convergence, convergence in probability, convergence in
  distribution, and the relations among them.
katex_macros:
  \ind: \operatorname{IND}
  \asconv: \xrightarrow{\text{a.s.}}
  \pconv: \xrightarrow{P}
  \dconv: \xrightarrow{d}
  \lrconv: \xrightarrow{L_r}
format:
  hugo-md:
    wrap: none
    toc: false
    code-fold: true
bibliography: refs.bib
citeproc: true
link-citations: true
reference-location: document
nocite: '@*'
execute:
  echo: true
  warning: false
  message: false
weight: 1
---


## Convergence Concepts

A sequence of random variables in $\R$ $X_n \to X$:

-   **In probability** if $\forall\,\epsilon>0,\ \mathbb{P}(|X_n - X| > \epsilon) \to 0$,
-   **Almost surely** if $\mathbb{P}(\lim_{n\to\infty} X_n = X) = 1$,
-   **In $\mathbf{L_r,r>0}$** if $\Eb|X_n-X|^r\rightarrow 0$,
-   **In distribution** if $F_n(x)=\Pb(X_n\le x)\rightarrow F(x)=\Pb(X\le x)\quad \forall x\in C(F)$, where $C(F)=\lbrace x|F\text{ is continuous at }x\rbrace$.

Note that, $\lbrace |X_n-X|>\epsilon \rbrace$ is nothing but $\lbrace \omega: |X_n(\omega)-X(\omega)|>\epsilon \rbrace$. Therefore $X_n,X$ when they converge in probability, almost surely or in $L_r$ need to be on the same probability space.

But for convergennce in distribution it is not necessary that $X_n$ and $X$ lie in the same probability space.

{{< theorem title="Cramer Wold Device" label="th-cramer-wold" >}} Suppose $X_n\in \R^k$ and $X_n\rightarrow X\Leftrightarrow \alpha^TX_n\xrightarrow{d} \alpha^TX\quad \forall \alpha\in \R^k$ {{< /theorem >}} The next theorem gives an equivalent definition for the almost sure convergence. {{< theorem >}} $X_n\xrightarrow{\text{a.s.}}X$ iff for every \$\>0 \$, $\lim\limits_{n\rightarrow \infty}\Pb(|X_k-X|>\epsilon\quad  \forall k\ge n)=1$ {{< /theorem >}} {{< proof >}} We can write $X_n\asconv X$ as $\Pb(\lim_{n\rightarrow \infty}X_n=X)=1$. Let, $A=\lbrace \lim_{n\rightarrow \infty}X_n=X\rbrace$. Fix $\omega \in A$. Fix $\epsilon>0$. Then, equivalently for $\epsilon>0, \exists  n$ such that $\forall k\ge n$, $|X_k-X|<\epsilon$. Therefore, we can write <span id="eq-1.1"></span> $$
\begin{equation}
\Pb(A)=\Pb\left(\lim_{n\rightarrow \infty}X_n=X\right)=\Pb\left(\bigcup_{\epsilon >0}\bigcap_{n=1}^{\infty}\bigcup_{k\ge n}\lbrace|X_k-X|<\epsilon\rbrace\right)=\Pb\left(\bigcup_{\epsilon >0}\bigcap_{n=1}^{\infty}A_n(\epsilon)\right),\tag{1.1}
\end{equation}
$$ where $A_n(\epsilon)=\bigcup_{k\ge n}\lbrace|X_k-X|<\epsilon\rbrace$. Now, as real line in dense with the set of the rational numbers, which are countable, we can write $$
\Pb\left(\bigcup_{\epsilon >0}\bigcap_{n=1}^{\infty}A_n(\epsilon)\right)=\Pb\left(\bigcup_{q\in \mathbb{Q}^{+}}\bigcap_{n=1}^{\infty}A_n(q)\right)
$$ Let, $q_1$ and $q_2$ are two rational numbers such that $q_1>q_2$. Note that if $\omega \in \bigcup_nA_n(q_2)\implies \omega \in \bigcup_nA_n(q_2)$. Therefore these sets, $\bigcup_nA_n(q)$ decreases as $q$ decreases. In other words, we have $$
\text{as } q\downarrow 0,\quad \bigcup_nA_n(q)\downarrow \bigcap_{q\in \mathbb{Q}^{+}}\bigcup_nA_n(q)
$$ Therefore, using continuity from below property of probability measures, we can say that $$
\Pb\left(\bigcup_nA_n(q)\right) \downarrow \Pb\left(\bigcap_{q\in \mathbb{Q}^{+}}\bigcup_nA_n(q)\right)=1
$$ Therefore, $$
\Pb\left(\bigcup_nA_n(q)\right) = 1 \quad \forall q\in \mathbb{Q}^{+}
$$ The vice-versa is also true as the limit of $1$'s will be 1. Now note that as $\R$ is dense, for all $\epsilon>0$, we can find a sequence of rational numbers, $q_n\rightarrow \epsilon$. Hence using continuity of measure we can say the following $$
\Pb\left(\bigcup_nA_n(\epsilon)\right) = 1 \quad \forall \epsilon >0
$$ It is easy to see that if we fix $\epsilon>0$, $A_n(\epsilon)\uparrow \bigcup_nA_n(\epsilon)$. Therefore, it is claimed that $$\lim_{n\rightarrow\infty}\Pb(A_n(\epsilon) )=\Pb\left(\bigcup_nA_n(\epsilon )\right) = 1
$$ {{< /proof >}} The next theorem is the definition only that gives an equivalent way to define the the **in probability** convergence. {{< theorem >}} $X_n\pconv X$ iff $\Pb(|X_n-X|>\epsilon)\rightarrow 0$ iff $\Pb(|X_n-X|\le \epsilon)\rightarrow 1$ {{< /theorem >}} The next theorem shows the relationships between different mode of convergence. {{< theorem >}} Suppose $\lbrace X_n\rbrace$ and $X$ are random variables defined on same probability space. Then the following are true

<ol type="i">
<li>
$X_n\asconv X \implies X_n\pconv X$
</li>
<li>
$X_n\pconv X\implies X_n\dconv X$
</li>
<li>
$X_n\lrconv X\implies X_n\pconv X$
</li>
</ol>
{{< /theorem >}}

{{< proof >}} Proof of (iii) follows from Markov's inequality, and the proof of (i) is a consequence of [Theorem 1.1](#theorem-1-1) and [Theorem 1.2](#theorem-1-2). We will prove the second part now.

Take $x\in C(F_X)$. Take $A=\lbrace X_n\le x\rbrace$. Fix $\omega \in A$. Fix any $\epsilon>0$. Then there will exist $N$, such that for all $n\ge N$, we shall have $|X_n-X|<\epsilon$. Hence we have $X<= x+\epsilon \mathbf{1}$ (where $\mathbf{1}=(1,1,\dots,1)\in \R^d$) for $n\ge N$ and we may have $|X_n-X|>\epsilon$ for some $k<N$. Therefore we have the following $$
\begin{align*}
& \lbrace X_n\le x\rbrace \subset \lbrace X\le x+\epsilon \mathbf{1} \rbrace \cup \lbrace |X_n-X|>\epsilon \rbrace \\\
\therefore \quad & \Pb(X_n\le x)\le \Pb(X\le x+\epsilon \mathbf{1})+\Pb(|X_n-X|>\epsilon) \\\
\implies& F_{X_n}(x)\le F_X(x+\epsilon \mathbf{1})+\Pb(|X-X_n|>\epsilon) \\\
\implies& \limsup_{n\rightarrow \infty}F_{X_n}(x)\le F_X(x+\epsilon \mathbf{1}) \tag{$\star$}
\end{align*}
$$

Similarly, we can say that $\lbrace X \le x - \epsilon \mathbf{1} \rbrace \subset \lbrace X_n\le x\rbrace \cup \lbrace |X_n-X|>\epsilon \rbrace$. Hence, we shall have the following $$
\begin{align*}
&F_X(x-\epsilon \mathbf{1})\le F_{X_n}(x)+\Pb(|X_n-X|>\epsilon)\\\
\implies & F_X(x-\epsilon \mathbf{1})\le \liminf_{n\rightarrow \infty}F_{X_n}(x)\tag{$\star\star$}
\end{align*}
$$ Combining $\star$ and $\star\star$ and using the continuity of $F_X$ at $x$, we get that $\lim\limits_{n\rightarrow \infty}F_{X_n}(x)=F_X(x)$. {{< /proof >}}

The next theorem is an important theorem, which will be used time and again in many contexts. {{< theorem title="Portmanteau Theorem" label="thm-Portmanteau" >}} Suppose a sequence of random variables $\lbrace X_n\rbrace$ is such that $X_n\rightarrow X$ in $\R^d$. Then the following are equivalent

<ol type="i">
<li>
$\Pb(X_n\le x)\rightarrow \Pb(X\le x)\quad \forall x\in C(F_X)$;
<li>
$\Eb[f(X_n)]\rightarrow \Eb[f(X)]\quad \forall$ bounded continuous function $f$;
<li>
$\Eb[f(X_n)]\rightarrow \Eb[f(X)]\quad \forall$ bounded Lipchitz function $f$;
<li>
$\liminf\limits_{n\rightarrow \infty}\Eb[f(X_n)]\ge \Eb[f(X)]\quad \forall$ nonnegative, continuous function $f$;
<li>
$\liminf\limits_{n\rightarrow \infty}\Pb(X_n\in G)\ge \Pb(X\in G)\quad \forall$ open set $G$;
<li>
$\limsup\limits_{n\rightarrow \infty}\Pb(X_n\in F)\le \Pb(X\in F)\quad \forall$ closed set $F$;
<li>
$\lim\limits_{n\rightarrow \infty}\Pb(X_n\in B)=\Pb(X\in B)\quad \forall$ Borel set $B$ with $\Pb(X\in \delta B)=0$, where $\delta B$ denotes the boundary set of B.
</ol>

{{< /theorem >}} {{< proof open="false">}} **i. $\implies$ ii.**

Note that from the first condition it is clear that for all rectangles, $I\in \R^d$, we will have $\Pb(X_n\in I)\rightarrow \Pb(X\in I)$. Fix $\epsilon >0$. Choose sufficiently large compact rectangle $I$ such that $\Pb(X\notin I)< \epsilon$. As $f$ is a continuous function, inside the rectangle $f$ is a uniformly continuous function. Let, $I=[a_1,b_1]\times \dots \times [a_d,b_d]$. Then there exists $\delta>0$ such that whenever $||x-y||<\delta ,x,y\in I$, $|f(x)-f(y)|< \epsilon$. Now, let $|a_{ij}-b_{ij}|<\frac{\delta}{\sqrt{d}}$ for $i=1,\dots ,d$. Then there will be finitely many one dimensional rectangles in each co-ordinate which will satisfy this. Hence, we will find finitely many $I_j's$ such that if $x,y\in I_j$, $|f(x)-f(y)|\epsilon$ and $I=\bigcup_j I_j$. Take $x_j\in I_j$ and define $f_{\epsilon}(x)=\sum_jf(x_j)I_j(x)$. Hence, on $I$, we have $|f-f_{\epsilon}|<\epsilon$. Now, $$
 \begin{align*}
& \left|\Eb[f(X_n)]-\Eb[f_{\epsilon}(X_n)]\right| \le  \left|\int_{X_n\in I}(f-f_{\epsilon})\right|+\left|\int_{X_n\notin I}f(X_n)\right|  \le & \epsilon+ M\Pb(X_n\notin I) \\\
& \left|\Eb[f(X)]-\Eb[f_{\epsilon}(X)]\right|\le \epsilon+ \Pb(X\notin I)\le 2\epsilon \\\
& \left|\Eb[f_{\epsilon}(X_n)]-\Eb[f_{\epsilon}(X)]\right|\le \sum_{j}\left|\Pb(X_n\in I)-\Pb(X\in I)\right||f(x_j)|
\end{align*}
 $$ Combining the above three inequalities, if we take $n\rightarrow \infty$, we shall have $$
 \left|\Eb[f(X_n)]-\Eb[f(X)]\right|< 5\epsilon
 $$ As, $\epsilon$ was arbitrary, we will have our desired result.

**ii. $\implies$ iii.**

All Lipchitz functions are continuous

**ii. $\Longleftrightarrow$ iv.**

To prove that the former one implies the later one, we need to approximate the non-negative continuous functions using bounded continuous functions and then we can use the part ii . Note that $f_m(x)=f(x)\wedge m$ is a bounded continuous function for any continuous function $f$. Therefore, we have $$
\Eb[f(X_n)\wedge m]\rightarrow \Eb[f(X)\wedge m]
$$ As, $0\le f_m\le f$, we also have, $\Eb[f(X_n)\wedge]< \Eb[f(X_n)]\quad \forall m,n$ and from the monotone convergence theorem, we can say that $\Eb[f(X)\wedge m]\uparrow \Eb[f(X)]$. Hence, we have the following result that $\liminf\limits_{n\rightarrow \infty}\Eb[f(X_n)]\ge \Eb[f(X)]$. For the converse, part it is sufficient to show that for any bounded continuous function, $g$, $\limsup\limits_{n\rightarrow \infty} \Eb[g(X_n)]\le \Eb[g(X)]$. Let, $g\le M_g$. As $M_g-g$ is a nonnegative continuous function, following iv. we shall have $$
\liminf_{n\rightarrow \infty}\Eb[M_g-g(X_n)]\le \Eb[M_g-g(X)]\implies \limsup_{n\rightarrow \infty} \Eb[g(X_n)]\le \Eb[g(X)] 
$$

**ii. $\implies$ vi.**

Let, $F$ be a closed set. $F^{\delta}=\lbrace x| d(x,F)<\delta \rbrace$ *(This is called the* $\delta$ *fattening of the set F)*. Consider the function $f_{\epsilon}(x)=\left(1-\frac{d(x,F)}{\epsilon}\right)\_{+}$. This function is uniformly continuous function and $F^{\delta}\downarrow F$ as $\delta\downarrow 0$. Now, we can show easily that $$
\mathbf{1}\_F\le f_{\epsilon} \le \mathbf{1}\_{F^{\epsilon}}
$$ Using this we can say that $$
\limsup_{n\rightarrow \infty} \Pb(X_n \in F)\le \limsup_{n\rightarrow \infty} \Eb[f(X_n)]\rightarrow \Eb f[X]\le \Pb(X \in F^{\epsilon}) \downarrow \Pb(X\in F)
$$

**v $\Longleftrightarrow$ vi**

Using the fact that if $F$ is closed $F^c$ is open and vice versa.

**v.+vi. $\implies$ vii.**

We know that $\bar{B}=B^{\circ}\bigcup \delta B$. $B^{\circ}$ is an open set. Then we shall have $$
\begin{align*}
& \Pb(X\in B^{\circ})\le \liminf_{n\rightarrow \infty} \Pb(X_n \in B^{\circ})\le \limsup_{n\rightarrow \infty} \Pb(X_n \in \bar{B}) \le \Pb(X\in \bar{B})\tag{$\star$} \\\
& \Pb(X\in B^{\circ})\le \Pb(X\in B)\le \Pb(X\in \bar{B})\tag{$\star\star$}
\end{align*}
$$ As, $\Pb(X\in \delta B)=0$, $\Pb(X\in B^{\circ})=\Pb(X\in \bar{B})$, the equality follows in $\star$ amd $\star\star$. Hence the result follows.

**vii. $\implies$ i.**

This follows trivially as we apply vii. with $B=\(-\infty,x\]$, where $\delta B=\lbrace x\rbrace$ and $x$ is a continuity point of $F_X$. {{< /proof >}} Portmanteau theorem is a useful theorem as we shall see and we shall be using the equivalent conditions of the week convergence now and then. The next theorem is continuous mapping theorem {{< theorem title="Continuous Mapping Theorem" label="thm-CMT ">}} Let, $X_n\in \R^k$ and $g$ be function from $\R^k$ to $\R^m$. Let, $D_g=\lbrace x\in \R^k: \text{ $g$ is discontinuous at $x$}\rbrace$. Let, $\Pb(X\in D_g)=0$. Then,

<ol type="i">
<li>
$X_n\xrightarrow{d}X \implies g(X_n)\xrightarrow{d}g(X)$;
<li>
$X_n\xrightarrow{P}X \implies g(X_n)\xrightarrow{P}g(X)$;
<li>
$X_n\xrightarrow{\text{a.s.}}X \implies g(X_n)\xrightarrow{\text{a.s.}}g(X)$;
<ol>
{{< /theorem >}}

{{< proof open="true" >}} **iii.** Note, that $\\{X_n \rightarrow g(X)\\}\subset \\{g(X_n) \rightarrow g(X)\\}\cup \\{X \in D_g\\}$. Hence, \$ \Pb(g(X_n) \rightarrow g(X))+\Pb(X \in D_g) \ge (X_n \rightarrow X)=1 \$. Hence, we have $\Pb(g(X_n)\rightarrow g(X))=1$. Thus $g(X_n)\asconv g(X)$.

**ii.** We know that $X_n\pconv X$ iff for every subsequence there exists a further subsequence with converges to the limiting distribution almost surely. Therefore, $$
\begin{align*}
& \exists \lbrace n_{k_i}\rbrace:\quad X_{n_{k_i}}\asconv X, \\\
\therefore\quad & \exists \lbrace n_{k_i}\rbrace:\quad g(X_{n_{k_i}})\asconv g(X)\\\
\therefore\quad & g(X_n)\pconv g(X)
\end{align*}
$$

**i.** Let $F$ be a closed set. As $X_n\dconv X$, by Portmanteau theorem we know that $\limsup\limits_{n\rightarrow \infty}\Pb(X_n\in F)\le \Pb(X\in F)$.

Now, $g^{-1}(F)$ may not be a closed set as we are not given the continuity of $g$. But $\overline{g^{-1}(F)}$ {{< /proof >}}
