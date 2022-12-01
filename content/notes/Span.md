---
title: "Span"
math: true
toc: true
---

## Definition
Let $S$ be a nonempty subset of a vector space $V$.\
The **span** of $S$, denoted $\text{span}(S)$ or $\langle S \rangle$,
is the set consisting of all linear combinations of the
vectors in $S$.

We define $\text{span}(\emptyset) = \lbrace 0 \rbrace$ for convenience.
A subset $S$ of a vector space $V$ **generates** (or **spans**) $V$
if $\text{span}(S) = V$.\
In this case, we also say that the vectors of $S$ generate (or span)
$V$.

## Theorems
### Theorem 1 *[^1]
>The span of any subset $S$ of a vector space $V$ is a [subspace](notes/Subspace.md) of $V$ that contains $S$.
>
>Moreover, any [subspace](notes/Subspace.md) of $V$ that contains $S$ must also contain $\text{span}(S)$.

### Proof
This result is immediate if $S = \emptyset$ because $\text{span}(\emptyset) = \lbrace \mathbf{0} \rbrace$, which is a subspace that contains $S$ and is contained in any subspace of $V$.

If $S \neq \emptyset$, then $S$ contains some vector $\mathbf{z}$; $0\mathbf{z} = \mathbf{0}$ is in $\text{span}(S)$.

Let $\mathbf{x}, \mathbf{y} \in \text{span}(S)$.
Then there exists vectors $\def\v#1{\mathbf{#1}} \v{u}\_1, \cdots, \v{u}\_m, \v{v}\_1, \cdots, \v{v}\_n$ in $S$ and scalars $a\_1, \cdots, a\_m, b\_1, \cdots, b\_n$

such that

$$
\def\v#1{\mathbf{#1}}
\begin{align*}
\v{x} = \sum\limits^m\_{i=1} {a\_i\v{u}\_i} \quad\text{and}\quad \v{y} = \sum\limits^n\_{i=1}{b\_i\v{v}\_i}.
\end{align*}
$$

Then, for any scalar $c$,

$$
\def\v#1{\mathbf{#1}}
c\v{x}+\v{y} = \sum\limits^m\_{i=1} {(ca\_i)\v{u}\_i} + \sum\limits^n\_{i=1}{b\_i\v{v}\_i}
$$

is clearly a linear combination of the vectors in $S$. Hence $c\mathbf{x}+\mathbf{y} \in \text{span}(S)$.
Thus $\text{span}(S)$ is a subspace of $V$.
Furthermore, if $\mathbf{v} \in S$, then $\mathbf{v} = 1\mathbf{v} \in \text{span}(S)$, so $S \subseteq \text{span}(S)$.

Now let $W$ denote any subspace of $V$ that contains $S$.
If $\mathbf{w} \in \text{span}(S)$, then $\mathbf{w}$ is a linear combination of 
some vectors $\mathbf{w}_1, \cdots, \mathbf{w}_k$ of $S$.
Since $S \subseteq W$, $\mathbf{w}_i \in W$ for all $i = 1, \cdots, k$. 
Therefore $\mathbf{w}$ is a linear combination of vectors of $W$, hence $\mathbf{w} \in W$. Thus $\text{span}(S) \subseteq W$.
$$\tag*{$||$}$$


[^1]: Linear Algebra, Fifth Edition, by Stephen Friedberg, Arnold Insel, and Lawrence Spence