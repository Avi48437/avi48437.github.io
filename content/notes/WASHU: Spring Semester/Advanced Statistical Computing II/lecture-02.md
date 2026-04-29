---
title: 'Lecture 2: Convexity, Geometry, and Differentiability in Optimization'
author:
  - name: Avinandan Roy
engine: knitr
date: 2026-01-10T00:00:00.000Z
math: true
summary: >-
  Introduces convex sets and functions, their geometric interpretation via level
  sets, and fundamental differentiability concepts (Fréchet and directional
  derivatives), highlighting their role in understanding optimization structure
  and behavior.
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
weight: 2
---


### Convex Sets and Convex Function

{{< definition title="Convex Set">}} A set $\Theta \subset \R^n$ is convex if for $\theta_1,\theta_2\in \Theta$ and for all $\lambda\in (0,1)$, $$
(1-\lambda)\theta_1+\lambda\theta_2\in \Theta
$$ {{< /definition >}} {{< example title="Hyperplanes are convex" >}} Let $\Theta=\lbrace \theta: a^T\theta=b\rbrace$, Prove that $\Theta$ is convex.

Let $\theta_1,\theta_2 \in \Theta$. Therefore, $a^T\theta_1=b$ and $a^T\theta_2=b$. Take $\lambda \in (0,1)$. $\therefore$ $a^T((1-\lambda)\theta_1+\lambda\theta_2)=(1-\lambda)b+\lambda b=b$. Hence, $((1-\lambda)\theta_1+\lambda\theta_2)\in \Theta$. So, $\Theta$ is convex. {{< /example >}}

{{< definition title="Convex function">}} Let $\Theta$ be convex. Let $f:\Theta \rightarrow \R$ be a differentiable function. Then $f$ is convex if $\forall \theta_1,\theta_2\in \Theta$, $\lambda\in (0,1)$, $$
f(\lambda\theta_1+(1-\lambda)\theta_2)\le \lambda f(\theta_1)+(1-\lambda)f(\theta_2)
$$

An equivalent definition can be given. With $\Theta$ convex and $f$ differentiable, $f$ is convex iff $f(\theta_2)\ge f(\theta_1)+\nabla f(\theta_1)^T(\theta_2-\theta_1)$ {{< /definition >}} {{< proof title="Proof of the first order characterization" >}} $\Rightarrow$

We know that $\forall \quad \theta_1,\theta_2\in\Theta$ and $\lambda\in(0,1)$, we have the following $$
\begin{aligned}
& \lambda f(\theta_2)+(1-\lambda)f(\theta_1)\ge f(\lambda\theta_2+(1-\lambda)\theta_1)\\\
\implies & \lambda(f(\theta_2)-f(\theta_1))\ge f(\lambda\theta_2+(1-\lambda)\theta_1)-f(\theta_1)\\\
\implies & \lambda(f(\theta_2)-f(\theta_1))\ge f(\theta_1+\lambda(\theta_2-\theta_1))-f(\theta_1)\\\
\implies & f(\theta_2)-f(\theta_1)\ge \frac{f(\theta_1+\lambda(\theta_2-\theta_1))-f(\theta_1)}{\lambda}\\\
\implies & f(\theta_2)-f(\theta_1)\ge ||\theta_2-\theta_1||_2\underbrace{\left(\frac{f(\theta_1+\lambda(\theta_2-\theta_1))-f(\theta_1)-\nabla f(\theta_1)^T(\theta_2-\theta_1)}{\lambda||\theta_2-\theta_1||_2}\right)}\_{\rightarrow 0 \text{ as }\lambda\rightarrow 0}\\\
&\hspace{12em}+\nabla f(\theta_1)^T(\theta_2-\theta_1)
\end{aligned}
$$ Therefore, we have the desired result.

$\Leftarrow$ Let, $\theta_1,\theta_2\in \Theta$. Then we are given that $f(\theta_2)\ge f(\theta_1)+\nabla f(\theta_1)^T(\theta_2-\theta_1)$.

Let, $\theta_{\lambda}=(1-\lambda)\theta_1+\lambda\theta_2$, when $\lambda\in (0,1)$ is fixed.Then, we can say that $$
 \begin{aligned}
 & f(\theta_1)\ge f(\theta_{\lambda})+\nabla f(\theta_{\lambda})   (\theta_1-\theta_{\lambda})\\\
 & f(\theta_2)\ge f(\theta_{\lambda})+\nabla f(\theta_{\lambda})(\theta_2-\theta_{\lambda})\\\
 \therefore & \lambda f(\theta_1)+(1-\lambda)f(\theta_2)\ge f(\theta_{\lambda})+\nabla f(\theta_1)^T((1-\lambda)\theta_1+\lambda\theta_2-\theta_{\lambda})\\\
 \therefore & \lambda f(\theta_1)+(1-\lambda)f(\theta_2)\ge f((1-\lambda)\theta_1+\lambda\theta_2)
 \end{aligned}
 $$ Therefore, $f$ is convex. {{< /proof >}}

Next we define the Level Sets, which will be useful to find an equivalent definition of the optimization problem;

### Level Sets

{{< definition title="Level Sets" >}} Let $f: \Theta\rightarrow \R$. For $c\in \R$, define the level set $L_{c}(f)=\\{\theta\in \Theta:\enspace f(\theta)=c \\}$ and the sublevel set $L^s_c(t)=\\{\theta \in \Theta:\enspace f(\theta)\le c\\}$. {{< /definition >}}

Then, it can be seen easily that $$
\min_{\theta\in \Theta}f(\theta) \Leftrightarrow \argmin_{c\in \R} \\{c:\enspace L_c(f)\neq \phi\\}
$$ {{< theorem  >}} If $f$ is convex, then $L_c^s(f)$ are also convex $\forall c$. {{< /theorem >}}

The idea of the level sets is to provide the geometric intuition underlying curvature.

-   round level sets $\implies$ curvature of $f$ is similar in all directions $\rightarrow$ well conditioned function.

-   elongated level sets $\implies$ curvature is steep in some directions and flat in others. $\rightarrow$ ill conditioned function.

{{< example title="Ill conditioned function" >}} Consider the function $f:\R^2\rightarrow \R$ such that $f(\theta)=\theta_1^2+100\theta_2^2$ {{< /example >}}

### Differentiability

{{< definition title="Frechet Differentiability" >}} A function $f:\R^p\rightarrow \R$ is Frechet differentiable at $\theta$ if there exists a vector $g\in \R^p$ such that $$
\lim_{h\rightarrow 0}\frac{f(\theta+h)-f(\theta)-g^Th}{||h||_2}=0
$$ and we denote this $g$ as $\nabla f(\theta)$. {{< /definition >}} {{< example title="Quadratic function $f(\theta)=\frac{1}{2}\theta^TA\theta+b^T\theta$ such that $A=A^T$" >}} Now, $f(\theta+h)=\frac{1}{2}(\theta+h)^TA(\theta+h)+b^T\theta=f(\theta)+\theta^TAh+\frac{1}{2}h^TAh+b^Th$. Therefore we have

$$
\frac{f(\theta+h)-f(\theta)-(\theta^TA+b^T)h}{||h||_2}=\frac{h^TAh}{2||h||_2}
$$

Note, that we can diagonalize $A$ as $A=Q\Lambda Q^T$, where $Q$ is a orthonormal matrix comprised of the eigenvectors corresponding to the eigenvalues of $A$ and $\Lambda$ is a diagonal matrix containing the eigenvalues. Hence, $$
\begin{aligned}
& h^TAh=h^TQ\Lambda Q^Th\le \lambda_{\max}(A)||h||_2^2\\\
\implies &  \frac{f(\theta+h)-f(\theta)-(\theta^TA+b^T)h}{||h||_2}=o(||h||_2)
\end{aligned}
$$ Therefore, we have that $f$ is Frechet differentiable and $\nabla f(\theta)=A\theta+b$. {{< /example >}} In the next example, we shall show that $l_1$ norm is convex but not Frechet-Differentiable.

{{< example title="$l_1$ norm is convex but not Frechet Differentiable" >}} We need to prove that $f(\theta)=||\theta||_1$ is not Frechet Differentiable.

Let's assume that it is Frechet Differentiable at $\theta\in \Theta$. Then there exists a $g\in \R^p$ such that $$
\begin{aligned}
& \frac{\sum_{i=1}^p(|\theta_i+h_i|-|\theta_i|)-g^Th}{||h||_2}\xrightarrow{h\rightarrow 0} 0 \\\
\implies & \sum\_{i=1}^p (|\theta\_i+h\_i|-|\theta\_i|)=g^Th+o(||h||\_2)
\end{aligned}
$$ Take $h=te_j$. Therefore, we will have that $$
|\theta_j+t|-|\theta_j|=tg^Te_j+o(|t|)
$$ Now take $\theta_j=0$. Then we will have $$
\operatorname{sign}(t)=g^Te_j+\frac{o(|t|)}{t}
$$ As the limit of the $LHS$ does not exists at $t=0$, $g$ can not exist. Hence $f$ is not Frechet Differentiable. {{< /example >}}

Nex, we will discuss the concept of directional derivative to tackle situations like Example 1.5

{{< definition title="Directional Derivative" >}} For a direction $v\in \R^p$, the directional derivative of $f$, at $\theta$ in direction $v$ is $$
D_vf(\theta)=\lim{t\downarrow 0}\frac{f(\theta+tv)-f(\theta)}{t}
$$ {{< /definition >}}

The next result shows that the Frechet Differentiability implies the directional derivative. {{< proposition >}} If $f$ is Frechet Differentiable at $\theta$, then for all $v\in \R^p$ $$
D_vf(\theta)=\nabla f(\theta)^Tv
$$ {{< /proposition >}} {{< proof >}} By definition of Frechet Differentiability, we have the following that $$
f(\theta+h)-f(\theta)=\nabla f(\theta)^Th+o(||h||_2)
$$ Substitute $h=tv$ and we will get $$
\begin{aligned}
& f(\theta+tv)-f(\theta)=t\nabla f(\theta)^Tv+o(||tv||_2)\\\
\therefore \enspace & \frac{f(\theta+tv)-f(\theta)}{t}=\nabla f(\theta)^Tv+\frac{o(|t|)}{t}
\end{aligned}
$$ Take $t\downarrow 0$ to get $D_vf(\theta)=\nabla f(\theta)^Tv$. {{< /proof >}}
