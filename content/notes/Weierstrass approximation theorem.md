---
title: "Weierstrass approximation theorem"
math: true
toc: true
---

## Theorem
> Let $f: \mathbb{R} \to \mathbb{R}$ be a continuous function on the interval $[a,b]$.
> Then, for any positive $\varepsilon$, there exists $n \in \mathbb{N}$ where for some 
> $n$-degree polynomial $p_n$,
> $\lVert f - p_n \rVert_{C^0} \leq \varepsilon$ holds.

## Proof
Without loss of generality, let $a=0$ and $b=1$. Since $f$ is continuous on $[0,1]$, let $M$ as:
$$
M = \sup\limits_{x \in [0,1]}|f(x)| := \lVert f \rVert_0.
$$

Consequently, for any $\xi \in [0,1]$, the following holds:
$$
|f(x)-f(\xi)| \leq
\begin{cases}
\dfrac{\varepsilon}{2} \qquad & &\text{if　} |x - \xi| < \delta \\
|f(x)| + |f(\xi)| &\leq 2M\\
&\leq 2M\cdot 1\\
&\leq 2M\left( \dfrac{|x - \xi|}{\delta} \right) ^2\qquad &\text{otherwise.}
\end{cases}
$$
Therefore we can conclude that 
$$
|f(x) - f(\xi)| \leq 2M\left( \dfrac{|x - \xi|}{\delta} \right) ^2 + \dfrac{\varepsilon}{2}.
$$

Now, we will prove that the polynomial of interest is actually the **[Bernstein polynomial](notes/Bernstein%20polynomial.md)**.

$$
\begin{aligned}
|B_n(x;f)-f(\xi)| &= |B_n(x;f) - B_n\left(x;f(\xi)\right)| = |B_n\left(x;f-f(\xi)\right)|\\
&= \left|\sum\limits_{\nu = 0}^n \left(f\left(\dfrac{\nu}{n}\right)-f(\xi)\right)\binom{n}{\nu}x^\nu (1-x)^{n-\nu}\right|\\
&\leq \sum\limits_{\nu = 0}^n \left|\,f\left(\dfrac{\nu}{n}\right)-f(\xi)\,\right|\binom{n}{\nu}x^\nu (1-x)^{n-\nu}\\
&= B_n\left(x;|f-f(\xi)|\right)\\
&\leq B_n\left(x; 2M\left( \dfrac{|x - \xi|}{\delta} \right) ^2 + \dfrac{\varepsilon}{2}\right)\\
&= \dfrac{2M}{\delta^2}\left( x^2+\dfrac{1}{n}(x - x^2) \right) - \dfrac{4M\xi}{\delta^2} + \dfrac{2M\xi^2}{\delta^2} + \dfrac{\varepsilon}{2}
\end{aligned}
$$
The last line is due to the [properties](notes/Bernstein%20polynomial.md###Properties) of Bernstein polynomials.

Next, let $\xi = x$. Then consequently,
$$
\begin{aligned}
|B_n(x;f) - f(x)|
&\leq \dfrac{2M}{\delta^2}\cdot\dfrac{\xi-\xi^2}{n} + \dfrac{\varepsilon}{2}\\
&\leq \dfrac{M}{2\delta^2}\cdot\dfrac{1}{n} + \dfrac{\varepsilon}{2}
\end{aligned}
$$
The last line is due to the fact that the maximum value of the function $x - x^2$ on the interval $[0,1]$ is $\dfrac{1}{4}$.

Finally, choose $n$ such that it satisfies $n \geq \dfrac{M}{\delta^2 \varepsilon}$. Then for any $x \in [0,1]$,
$$
|B_n(x;f)-f(x)| \leq \varepsilon
$$
and equivalently,
$$
\lVert B_n(\cdot;f) - f\rVert_{C^0} \leq \varepsilon.
$$
This completes the proof.
$$\tag*{$||$}$$