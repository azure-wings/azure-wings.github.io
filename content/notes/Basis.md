---
title: "Basis"
math: true
toc: true
---

## Definition
>Let $V$ be a [vector space](notes/Vector%20space.md) and $\beta$ be a subset of $V$.\
>If $\beta$ is [linearly independent](notes/Linear%20independence.md) and [spans](notes/Span.md) $V$, then $\beta$ is a **basis** of $V$.\
>We can also say that $\beta$ forms a basis for $V$.

## Theorems
### Theorem 1
>Let $V$ be a vector space over a [field](notes/Field.md) $F$, and $\def\v#1{\mathbf{#1}} \v{u}\_1, \cdots, \v{u}\_n$ be $n$ distinct vectors of $V$.\
>Then $\def\v#1{\mathbf{#1}} \beta = \lbrace \v{u}\_1, \cdots, \v{u}\_n \rbrace$ forms a basis for $V$ if and only if an arbitrary vector $\mathbf{v} \in V$ can be **uniquely** written as a linear combination of vectors of $\beta$.\
>In other words, $\exists! a\_1, \cdots, a\_n \in F$ such that $\def\v#1{\mathbf{#1}} \v{v} = \sum\limits^n\_{i=1} a\_i\v{u}\_i$.

### Proof
