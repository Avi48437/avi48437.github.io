---
title: 'Lecture 1: Optimization Basics and Existence of Solutions'
author:
  - name: Avinandan Roy
engine: knitr
date: 2026-01-10T00:00:00.000Z
math: true
summary: >-
  Defines optimization problems and key concepts (global/local minima,
  stationary points), and gives conditions—via lower semicontinuity,
  compactness, or coercivity—under which minimizers exist, with implications for
  statistical estimation and algorithms.
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


## What is an Optimization Problem?

{{< setsection 1 >}}

Let us first formally define what we mean by an optimization problem first. {{< definition title="Optimization Problem" >}} An optimization problem consists of

-   a decision variable $\theta \in \R^p$,
-   a feasible set $\Theta \subset \R^p$,
-   an objective function $f:\R^p\rightarrow \R\cup\lbrace \pm \infty \rbrace$ and
-   finding $\argmin\limits_{\theta \in \Theta} f(\theta)$

This $f(\theta)$ is called the objective value and $\theta$ is a candidate solution. {{< /definition >}}

{{< example title="OLS">}} An example of such optimization problem is - *Ordinary Least Square Solution of Linear Regression*. Note that we have the model $Y=X\beta +\epsilon$. Here the decision variable is $\beta$, the feasible set is $\R^p$ and the objective function is the $L_2$ loss between $Y$ and $X\beta$, which is $||Y-X\beta||^2\_2$ {{< /example >}}

Now, we shall discuss what about constrained vs. unconstrained Optimization. For that let us first define what we call an indicator function {{< definition title="Indicator Function" >}} The indicator function $i_{\Theta}:\Theta\rightarrow \lbrace 0,\infty\rbrace$ such that $$
i_{\Theta}(\theta)=\begin{cases}
                          0,\quad\theta \in \Theta \\\
                          \infty,\quad \theta \notin \Theta
                         \end{cases}
$$ Suppose then the constrained space is $\Theta^{\*}\subset \Theta$. We can then write that $$
\min_{\theta \in \Theta}f(\theta)\Leftrightarrow \min_{\theta \in \Theta^{\*}}f(\theta)+i_{\Theta}(\theta)
$$ {{< /definition >}}

### Global, Local, Stationary points

Now, it may be possible that in a minimization problem more than one mode exits for the objective function. In that case we define the *Global Minimizer, Local Minimizer* and to find out the existence of the optimizers, we find where the slope of the objective function becomes zero and hence we define the *Stationary Point*

{{< definition title="Global Minimizer, Local Minimizer, Stationary Point" >}}

-   a point $\theta^{\*}$ is called the **Global Minimizer** if, $$
    \boxed{f(\theta^{\*})\le f(\theta),\quad \forall \theta\in \Theta}
    $$
-   a point $\theta^{\*}$ is called the **Local Minimizer** if, $$
    \boxed{\exists \enspace r>0\text{ such that  } f(\theta^{*})\le f(\theta)\enspace \forall \theta\in B(\theta^{\*},r)\cap \Theta}
    $$ where $B(\theta,r)=\rbrace \phi: ||\theta-\phi||\le r\rbrace$,
-   a point $\theta^{\*}$ is called a **Stationary Point** if $f$ is differentiable at $\theta^{\*}$ and satisfies $$
    \boxed{\nabla f(\theta^{\*})=0}
    $$  
    {{< /definition >}} We can similarly define the *Global Maximizer* and *Local Maximizer*.

### Existence: Why Solutions exists or not?

Semicontinuous functions are at the heart of this topic. So, we will first define what is semicontinuity. We will define both lower semicontinuous function and upper semicontinuous function here. {{< definition title="Lower Semicontinuous (LSC) and Upper Semicontinuous (USC) functions" >}} Let, $(\Theta,d)$ be a metric space abd $f:\Theta\rightarrow \R$. The function $f$ is **lower semicontinuous** at $\theta \in \Theta$ if for every sequence $\lbrace\theta_n\rbrace$ such that $\theta_n\rightarrow \theta$, we have $$
f(\theta)\le \liminf_{n\rightarrow \infty}f(\theta_n)
$$ and $f$ is **upper semicontinuous** at $\theta \in \Theta$ if for every sequence $\lbrace\theta_n\rbrace$ such that $\theta_n\rightarrow \theta$, we have $$
f(\theta)\ge \limsup_{n\rightarrow \infty}f(\theta_n)
$$ {{< /definition >}} Here are couple of more definitions below {{< definition title="Coercive function">}} A function $f:\Theta\rightarrow \R$ is **coercive** if $||\theta||\rightarrow \infty\enspace \implies f(\theta)\rightarrow \infty$ {{< /definition >}}

{{< definition title="Closed Set">}} Let, $(\Theta,d)$ be a metric space. $\Theta$ is said to be a closed set if for every sequence $\lbrace \theta_n \rbrace \subset \Theta$, such that $\theta_n\rightarrow \theta$, we have $\theta\in \Theta$. {{< /definition >}}

{{< definition title="Compact Set (Heine-Borel)">}} $\Theta$ is compact if is closed and bounded. (*Note that this characterization works only when the underlying space is finite-dimensional.*). The **sequential definition** of compactness is as follows: $\Theta$ is compact iff every sequence in $\Theta$ has a further subsequence with converges to limit point inside $\Theta$. {{< /definition >}}

{{< theorem subtitle="Existence of minimizers on closed sets" >}} Let $\Theta$ be nonempty and closed. Assume $f:\Theta\rightarrow \R$ is lower semicontinuous on $\Theta$ and either $\Theta$ is compact or $f$ is coercive on $\Theta$, then the problem $\min\limits_{\theta\in \Theta}f(\theta)$ attains a minimizer. {{< /theorem >}}

{{< proof >}} **case 2**

Given that $\Theta$ is closed and $f$ is coercive. Let, us first define the level sets. $$
L_c=\lbrace \theta\in\Theta : f(\theta)\le c\rbrace
$$ Note that $L_c$ is bounded for all c. If not bounded then then due to coerciveness when $||\theta||\rightarrow \infty$ inside $L_c$, $f(\theta)\rightarrow \infty$. But this contradicts the condition inside $L_c$, that $f(\theta)\le c$. Therefore, $L_c$ is a bounded set. Let $\lbrace \theta_n\rbrace$ a sequence such that $\theta_n\rightarrow \theta$. As $f$ is lower semicontinuous, $\liminf\limits_{n\rightarrow \infty}f(\theta_n)\ge f(\theta)$. Therefore $f(\theta)\le c$ and as $\Theta$ is closed, $\theta \in L_c$. So, $L_c$ is closed and bounded and hence $L_c$ is compact.

Let, $m=\inf f(\theta)$. Consider a sequence $\lbrace \theta_k\rbrace\subset \Theta$ such that $f(\theta_k)\downarrow m$. Now there will exist $K$ such that for all $k\ge K$, $f(\theta_k)\le m+1$. Hence $\lbrace \theta_l\rbrace\_{l\ge K}\subset L_{m+1}$. As $L_{m+1}$ is compact this sequence $\lbrace \theta_l\rbrace\_{l\ge K}$ will have a further subsequence, $\lbrace \theta^{\'}_k\rbrace$ that will converge to a limit point $\theta^{\*}$.

Hence, by lower semicontinuity of $f$, we shall get the following $$
f(\theta^{\*})\le \liminf_{k\rightarrow \infty}f(\theta'_k)=m
$$ {{< /proof >}} {{< example >}} Let, $\Theta = (0,1)$ and $f(\theta)=\theta$. Note that the minimizer does not exist in $\Theta$. {{< /example >}}

Many estimators are defined as solutions to optimize problems like $\min\limits_{\theta \in \Theta}f(\theta)$. Existence theorems are nice but they don't tell us anything about how to solve the problem.

In statistical computation, estimation problems are typically formulated as the minimization of an objective function (e.g., a negative log-likelihood or penalized loss) over a parameter space. Numerical algorithms implicitly assume that this optimization problem is well posed, meaning that a minimizer exists and can be approximated by iterative procedures. The following theorem provides conditions under which this assumption is mathematically justified.

-   **Existence of estimators:** Ensures that statistical objectives attain a minimizer, rather than merely an unattained infimum.
-   **Stability of numerical algorithms:** Compactness or coercivity prevents minimizing sequences from diverging to infinity, avoiding numerical blow-up.
-   **Role of regularization and priors:** Penalties and Bayesian priors enforce coercivity, resolving non-existence pathologies in MLEs (e.g., separation or variance collapse).
-   **Feasibility of algorithmic limits:** Closedness of the parameter space guarantees that limits of convergent iterates remain admissible.
-   **Meaningful convergence diagnostics:** Lower semicontinuity ensures that convergence of objective values corresponds to convergence toward a valid minimizer.
-   **Foundation for algorithmic guarantees:** Provides the mathematical conditions implicitly required by EM, SAEM, gradient descent, and second-order optimization methods.
