---
title: "Bernstein polynomial"
math: true
toc: true
---

A **Bernstein polynomial** is a polynomial that is a [linear combination](notes/Linear%20combination.md) of Bernstein [basis](notes/Basis.md) polynomials.

## Definition
The $n +1$ **Bernstein basis polynomials** of degree $n$ are defined as
> $b_{\nu, n}(x) = \binom{n}{\nu}x^\nu (1-x)^{n-\nu}, \qquad \text{where}\; \nu = 0, \cdots, n$.

The name is from the fact that the Bernstein basis polynomials of degree $n$ form a [basis](notes/Basis.md) for the [vector space](notes/Vector%20space.md) $\mathbb{P}_n$, a space which consists of polynomials with degree at most $n$. 

A **Bernstein polynomial** is a linear combination of Bernstein basis polynomials:
> $B_n(x) = \sum\limits_{\nu = 0}^n \beta_\nu b_{\nu, n}(x)$

where the coefficients $\beta_\nu$ are called **Bernstein coefficients**.

## Examples
### Approximation of continuous functions
Let $f$ be a continuous funciton on the interval $[0,1]$. Let $\beta_\nu = f\left(\dfrac{\nu}{n}\right)$.
We can denote the corresponding Bernstein polynomial as $B_n(x; f)$.
The corresponding Bernstein polynomial becomes:
$$
\begin{aligned}
B_n(x; f) &= \sum\limits_{\nu = 0}^n f\left(\dfrac{\nu}{n}\right)b_{\nu, n}(x)\\
&= \sum\limits_{\nu = 0}^n f\left(\dfrac{\nu}{n}\right)\binom{n}{\nu}x^\nu (1-x)^{n-\nu}.
\end{aligned}
$$


## Properties
### Property #1
> $B_n(x; \mathbb{1}) = 1$

### Property #2
> $B_n(x;x) = x$

### Property #3
> $B_n(x;x^2) = x^2 + \dfrac{1}{n}(x - x^2)$

### Property #4
> $B_n(x; af + g) = aB_n(x; f) + B_n(x;g)$
