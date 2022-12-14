---
title: "Functional dependency"
math: true
toc: true
---

There are usually a variety of constraints on the data in the real world.

An instance of a relation that satisfies all such real-world constraints is called a **legal instance** of the relation; a legal instance of a database is one where all the relation instances are legal instances.

Some of the most commonly used types of real-world constraints can be represented formally as [[notes/Keys|keys]] (superkeys, candidate keys, and primary keys), or as **functional dependencies**.

## Definition

Consider a relation schema $r(R)$, and let $\alpha, \beta \subseteq R$ be sets of attributes.

Given an instance of $r(R)$, the instance is said to satisfy a **functional dependency** $\alpha \to \beta$ if for all pairs of tuples $t_1$ and $t_2$ in the instance, 
$$
t_1[\alpha] = t_2[\alpha] \Rightarrow t_1[\beta] = t_2[\beta].
$$

The functional dependency $\alpha \to \beta$ is said to **hold** on schema $r(R)$ if every legal instance of $r(R)$ satisfies the functional dependency.

One easy way to understand the concept of functional dependency is to interpret $\alpha \to \beta$ as: 
> If values of $\alpha$ is given, then values of $\beta$ is _uniquely_ determined.

## Trivial functional dependencies

A functional dependency is **trivial** if it is satisfied by all instances of a relation.

In general, $\alpha \to \beta$ is trivial if $\beta \subseteq \alpha$.

## Keys and functional dependencies

- $K$ is a superkey for relational schema $r(R)$ if and only if the functional dependency $K \to R$ holds on $r(R)$.
- $K$ is a candidate key for $r(R)$ if and only if the functional dependency $K \to R$ holds on $r(R)$, and for any $L \subsetneq K$, $L \not\to R$.

## Use of functional dependencies

Functional dependencies can be used to:
- Test relations to see if they are legal inder a given set of functional dependencies
- Specify constraints on the set of legal relations

Note that a specific instance of a relation schema may satisfy a functional dependency even if the functional dependency **does not** hold on all legal instances.
- e.g., A specific instance of `instructor` may, **by chance**, satisfy $\texttt{name} \to \texttt{ID}$