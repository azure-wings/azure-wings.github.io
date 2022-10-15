---
title: "Vector space"
math: true
---

## Definition

A vector space $V$ over a [field](notes/Field.md) $F$ consists of a set on which two operations $+$ (_addition_) and $\cdot$ (_scalar multiplication_) are defined so that the followings hold.

For any $\mathbf{x}, \mathbf{y}, \mathbf{z} \in V$ and $c, d \in F$:
> **(A1)** $\mathbf{x}, \mathbf{y} \in V \Rightarrow \mathbf{x} + \mathbf{y} \in V$
>
> **(A2)** $\mathbf{x} + \mathbf{y} = \mathbf{y} + \mathbf{x} \quad$ (Commutativity of addition)
>
> **(A3)** $(\mathbf{x} + \mathbf{y}) + \mathbf{z} = \mathbf{x} + (\mathbf{y} + \mathbf{z}) \quad$ (Associativity of addition)
>
> **(A4)** $\exists ! \mathbf{0} \in V$ such that $\forall \mathbf{x} \in V: \mathbf{x} + \mathbf{0} = \mathbf{x} \quad$ (Existence of additive identity)
>
> **(A5)** $\forall \mathbf{x} \in V: \exists ! (-\mathbf{x}) \in V$ such that $\mathbf{x} + (-\mathbf{x}) = \mathbf{0} \quad$ (Existence of additive inverse)
>
> **(M1)** $\mathbf{x} \in V \Rightarrow c\mathbf{x} \in V$
>
> **(M2)** $c(d\mathbf{x}) = (cd)\mathbf{x}$
>
> **(M3)** $c(\mathbf{x} + \mathbf{y}) = c\mathbf{x} + c\mathbf{y}$
>
> **(M4)** $(c + d)\mathbf{x} = c\mathbf{x} + d\mathbf{x}$
>
> **(M5)** $\forall \mathbf{x} \in V: 1\mathbf{x} = \mathbf{x}$

## Examples
### The space of $m \times n$ matrices
Let $F$ be any field and $m, n \in \mathbb{N}$. Define $F^{m\times n}$ as the set of all $m\times n$ matrices over the field $F$. Then, for any matrices $A, B \in F^{m \times n}$ and scalar $c \in F$,
- $(A + B)\_{ij} = A\_{ij} + B\_{ij}$
- $(cA)\_{ij} = cA\_{ij}$

### The space of functions from a set to a field
Let $F$ be any field, and $S$ be any nonempty set. Define $V$ as the set of all functions $S \to F$. Then, for any functions $f, g \in V$ and scalar $c \in F$, $\forall s \in S$:
- $(f + g)(s) = f(s) + g(s)$
- $(cf)(s) = cf(s)$
- The zero vector is the function $\mathbf{0}: S \to \{0\}$.
- The inverse vector $(-f)$ of an arbitrary function $f \in V$ is given as $(-f)(s) = -f(s)$.

### The space of polynomial functions over a field
Let $F$ be any field. Define $V$ as tje set of all polynomials $F \to F$, that is, all functions $f: F \to F$ in the form of
$$f(x) = \sum\limits_{i=0}^n c_ix^i$$
where $c_i \in F$ $(i= 0, \cdots, n)$ are independent of $x$.


## Related Concepts
- [Norm](notes/Norm.md): Defines a distance-like property in vector spaces
- [Inner product](notes/Inner%20product.md): Allows the concept of 'direction' to be considered in vector spaces
 