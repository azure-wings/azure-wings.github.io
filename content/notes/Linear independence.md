---
title: "Linear independence"
math: true
toc: true
---

## Definition
A subset $S$ of a vector space $V$ is called **linearly dependent** if
there exist a finite number of distinct vectors $\mathbf{u}_1, \cdots, \mathbf{u}_n$ in $S$
and scalars $a_1, \cdots, a_n$, _not all zero_, such that

$$\sum\limits\_{i=1}^n a\_i\mathbf{u}\_i = \mathbf{0}.$$

In this case we also say that the vectors of $S$ are linearly dependent.

A subset $S$ of a vector space $V$ that is not linearly dependent is called **linearly independent**.
We also say that the vectors of $S$ are linearly independent.

## Theorems
### Theorem 1
>Let $V$ be a vector space over a field $F$, and let $S_1 \subseteq S_2 \subseteq V$.
>
>If $S_1$ is linearly dependent, then $S_2$ is also linearly dependent.

### Proof
Since $S\_1$ is linearly dependent, we can choose some vectors $\def\v#1{\mathbf{#1}} \v{v}\_1, \cdots, \v{v}\_n$ such that for some scalars $a\_1, \cdots, a\_n$,

$$
\def\v#1{\mathbf{#1}}
\sum\limits\_{i = 1}^n a\_i\v{v}\_i = \v{0}.
$$

Then, since $S\_1 \subseteq S\_2$, we know that $\v{v}\_i \in S\_2$ for all $i = 1, \cdots, n$. Hence by definition the vectors of $S\_2$ are linearly dependent.
$$\tag*{$||$}$$ 

### Corollary
>Let $V$ be a vector space over a field $F$, and let $S_1 \subseteq S_2 \subseteq V$.
>
>If $S_2$ is linearly independent, then $S_1$ is also linearly independent.

### Theorem 2
>Let $S$ be a linearly independent subset of a vector space $V$, 
>and let $\mathbf{v}$ be a vector in $V$ that is not in $S$.
>
>Then $S \cup \{\mathbf{v}\}$ is linearly dependent 
>if and only if $\mathbf{v} \in \text{span}(S)$.