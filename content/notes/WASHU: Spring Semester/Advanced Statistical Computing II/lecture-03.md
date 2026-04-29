---
title: 'Lecture 3: Gradient Geometry and Iterative Optimization'
author:
  - name: Avinandan Roy
engine: knitr
date: 2026-01-10T00:00:00.000Z
math: true
summary: >-
  Explains the geometric role of gradients as directions of steepest
  ascent/descent, their relation to level sets, and motivates iterative
  optimization via local linear approximations and descent methods.
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
weight: 3
---


### Gradient geometry: steepest ascent and descent

Once a gradient exists, we can ask a more refined geometric question:

Among all directions of a fixed length, which direction increases the function the fastest?

{{< theorem title="Cauchy-Schwartz inequality" >}} For any vectors $x,y\in \R^p$, we have $$
|x^Ty|\le ||x||_2||y||_2
$$ Moreover equality holds if and only if $x$ and $y$ are linearly dependent which is to say that $x=\lambda y$ for some scalar $\lambda\in \R$. {{< /theorem >}} To isolate direction rather than scale, we restrict attention to unit vectors. {{< theorem title="Gradient vectors as steepest ascent" >}} Let, $f$ be differentiable at $\theta$. Among all directions $v$, with $||v||_2=1$, $$
\max\limits\_{||v||_2=1}\nabla f(\theta)^Tv=||\nabla f(\theta)||_2
$$ and the maximizer is $u=\frac{\nabla f(\theta)}{||f(\theta)||_2}$ when $\nabla f(\theta)\neq 0$ {{< /theorem >}} {{< proof >}} By Cauchy Schwartz inequality we will have $$
\nabla f(\theta)^Tv\le ||\nabla f(\theta)||\_2\underbrace{||v||\_2}_{=1}=||\nabla f(\theta)||\_2
$$ {{< /proof >}}

This above theorem essentially tells us that the gradient points in the direction of the maximal instantaneous increase of the function and the magnitude $||\nabla f(\theta)||_2$ is the maximal rate of increase per unit step.

#### Steepest descent direction

While finding the minimizer of an objective function, we want **steepest decrease** and that's why the direction of the steepest decrease is the negative gradient $-\nabla f(\theta)$. his is the fundamental geometric justification for gradient descent updates of the form $$
\theta^{(k+1)}=\theta^{(k)}-\eta_k\nabla f(\theta^{(k)})
$$

#### Connection to level sets

Level sets provide a geometric interpretation of gradients and directional derivatives. Let \$ f : \mathbb{R}^p \rightarrow \mathbb{R} \$ be a differentiable function.  
The **level set** of \$ f \$ at height \$ c \$ is defined as $$
\mathcal{L}_c = \\{ \theta \in \mathbb{R}^p : f(\theta) = c \\}.
$$

Intuitively, a level set consists of all points in parameter space where the function takes the same value. Moving along a level set does not change the value of the function.

Let $\theta(t)$ be a smooth curve that lies entirely on a level set $\mathcal{L}_c$. Then $$
f(\theta(t)) \equiv c \quad \text{for all } t.
$$ Differentiating both sides with respect to \$ t \$ and applying the multivariable chain rule gives $$
\frac{d}{dt} f(\theta(t))
= \nabla f(\theta(t))^\top \theta'(t)
= 0.
$$

This equation holds for **any** smooth curve tangent to the level set. Therefore, the gradient $\nabla f(\theta)$ is orthogonal to every tangent direction $\theta'(t)$ along the level set. In other words, the gradient is **normal (perpendicular)** to the level set at $\theta$. This geometric fact describes that moving along the level set produces no change in the function value, so the direction of maximum increase must be perpendicular to it.

### Local Linear Models and Descent

In nearly all statistical objectives, the minimizer cannot be written in closed form. Even when $f$ is convex, the equation defining an optimum (e.g. $\nabla f(\theta)=0$) may not admit an analytic solution, and solving it exactly can be as hard as the original problem. This motivates *iterative* algorithms: procedures that generate a sequence $\\{\theta\^{(k)}\\}\_{k\ge 0}$ intended to converge to a solution.

{{< definition title="Iterative optimization algorithm" >}} An *iterative optimization algorithm* is a rule that generates a sequence $\\{\theta\^{(k)}\\}\_{k\ge 0}$ according to $$
\theta^{(k+1)}=\mathcal{A}(\theta^{(k)}; \text{ information about } f\text{ near }\theta^{(k)}),
$$ where $\mathcal{A}$ is the update map. {{< /definition >}}

#### Why are iterative optimization algorithms local ?

-   In practice we don't know how $f$ behaves across the global landscape $\Theta$.
-   Start with $\theta^{(k)}$, we can often calculate $f(\theta^{(k)})$.
-   $\nabla f(\theta^{(k)})$: we often can compute or approx.

#### Linearization as a principled local surrogate

First, recall the implication of a function being **Fréchet differentiable**.  
Let $f : \mathbb{R}^p \to \mathbb{R}$ be Fréchet differentiable at $\theta$. By definition, there exists a gradient $\nabla f(\theta)$ and a remainder term $r_\theta(h)$ such that

$$
f(\theta + h) = f(\theta) + \nabla f(\theta)^\top h + r_\theta(h),
\text{ with }
\frac{r_\theta(h)}{||h||_2} \to 0 \quad \text{as } h \to 0.
$$

Equivalently, for every $\epsilon > 0$ there exists $\delta > 0$ such that

$$
|f(\theta+h)-f(\theta)-\nabla f(\theta)^T h| \le \epsilon ||h||_2\text{ whenever } ||h||_2 \le \delta.
$$

{{< definition title="Local Linear Model" >}} The local linear model of $f$ at $\theta$ is $$
m_{\theta}(h):=f(\theta)+\nabla f(\theta)^Th
$$ {{< /definition >}}

The above inequality hows that on a sufficiently small neighborhood, the true objective differs from its linear model by at most $O(||h||\_2)$. Thus, minimizing $m_{\theta}(h)$ over small steps is a principled approximation to minimizing the true objective locally.

#### Steepest descent as a geometric optimization problem

For Frechet differentiable function, $f$, we have $$
\min_{||u||\_2=1}D\_uf(\theta)=\min_{||u||\_2=1}\nabla f(\theta)^Tu.
$$ {{< theorem title="Steepest descent direction" >}} If $\nabla f(\theta)\neq 0$, then $$
\min\_{||u||_2=1}\nabla f(\theta)^Tu=-||\nabla f(\theta)||_2
$$ {{< /theorem>}}' Proof of the above theorem follows directly from Cauchy-Schwartz inequality.

#### Why the steepest descent direction guarantees decrease ?

Directional derivatives describe infinitesimal behavior. We now show that sufficiently small steps in the steepest descent direction produce an actual decrease in the objective.

{{< proposition title="Local Decrease along steepest descent" >}} Suppose $f$ is Frechet differentiable at $\theta$ and $\nabla f(\theta)\neq 0$. Let $$
u^{\*}=-\frac{\nabla f(\theta)}{||\nabla f(\theta)||_2}
$$ Then there exists $t_0$ such that for all $t\in (0,t_0)$, $$
f(\theta+tu^{\*})<f(\theta)
$$ {{< /proposition >}} {{< proof >}} By, Frechet Differentiability, we have $$
\begin{aligned}
& f(\theta+tu^{\*})=f(\theta)+t\nabla f(\theta)^Tu^{\*}+o(t)\\\
\implies & f(\theta+tu^{\*})=f(\theta)-t||\nabla f(\theta)||_2+o(t)
\end{aligned}
$$ as $\frac{o(t)}{t}$ goes to $0$ as $t\rightarrow 0$, there exist $t_0$ such that $\forall t\in (0,t_0) \enspace, |o(t)|\\le \frac{t||\\nabla f(\theta)||\_2}{2}$ and hence the result follows. {{< /proof >}}
