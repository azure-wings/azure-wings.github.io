---
title: "Subspace"
math: true
toc: true
---

## Definition
> Let $V$ be a [vector space](notes/Vector%20space.md) over the [field](notes/Field.md) $F$. A **subspace** of $V$ is a subset $W \subset V$ which itself is a vector space over $F$ with the same operations defined on $V$.

## Observations
### Observation 1
>In any vector space $V$, $V$ and $\lbrace \mathbf{0} \rbrace$ are subspaces of $V$.
>The latter is called the **zero subspace** of $V$.

## Theorems
### Theorem 1 *[^1]
> A non-empty subset $W$ of $V$ is a subspace of $V$ _if and only if_ $\forall \mathbf{x}, \mathbf{y} \in W, \forall c \in F:$ $c\mathbf{x} + \mathbf{y} \in W$.

### Proof
$(\Rightarrow)$ Trivial.

$(\Leftarrow)$ Since $W \neq \emptyset$, $\forall \mathbf{v} \in W:$ $(-1)\mathbf{v} + \mathbf{v} = \mathbf{0} \in W$.

$\forall \mathbf{w} \in W, \forall c \in F:$ $c\mathbf{w} = c\mathbf{w} + \mathbf{0} \in W$. In particular, $(-1)\mathbf{w} = -\mathbf{w} \in W$.

Finally, $\forall \mathbf{v}, \mathbf{w} \in W:$ $\mathbf{v} + \mathbf{w} = 1\mathbf{v} + \mathbf{w} \in W$.

Therefore, $W$ is a subspace of $V$.
$$\tag*{$||$}$$
### Theorem 2 *[^1]
> The intersection of any collection of subspaces of a vector space $V$ is a subspace of $V$.

### Proof
Let $\lbrace W\_a \rbrace$ be the collection of subspaces of $V$, and let $W = \cap\_{a}W\_a$. Since $\mathbf{0} \in W\_a$ for all $W\_a$, $\mathbf{0} \in W$ and thus $W$ is nonempty.

Let $\mathbf{x}, \mathbf{y} \in W$ and $c$ be an arbitrary scalar. By definition of $W$, $\mathbf{x},\mathbf{y} \in W\_a$ for all $W\_a$ and since they are all subspaces of $V$, $c\mathbf{x} + \mathbf{y} \in W\_a$ for all $W\_a$. Thus $c\mathbf{x} + \mathbf{y} \in W$. 
$$\tag*{$||$}$$ 

[^1]: Linear Algebra, Second Edition, by Kenneth Hoffman and Ray Kunze