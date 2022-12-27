---
title: "Dependency preservation"
math: true
toc: true
---

## Overview

Testing [[notes/Functional dependency|functional dependency]] constraints each time the database is updated can be costly. Thus, it is useful to design the database in a way that constraints can be tested efficiently.

When decomposing a relation, it may be no longer possible to do the testing without having to perform a [[notes/Relational algebra#Cartesian Product|Cartesian product]] of [[notes/Relational algebra#Join|join]] operations.

A decomposition that makes it computationally hard to enforce functional dependency is said to be _not_ **dependency preserving**. 

Conversely, if functional dependencies of the original relation can be checked on the decomposed relations without the need of Cartesian product or join operations, is said to be **dependency preserving**.

## Definition

Let $F$ be the set of functional dependencies on schema $R$, and let $R_1, \cdots, R_n$ be a decomposition of $R$. Let $F_i$ be a [[notes/Restriction(Database)|restriction]] of $F$ to $R_i$.

The decomposition is **dependency preserving** if the following holds:

$$
\left( \bigcup_{i=1}^n F_i \right)^+ = F^+
$$

Testing for dependency preservation using the above definition takes exponential time.

## Algorithm for testing dependency preservation

The following algorithm checks if a dependency $\alpha \to \beta$ is preserved in a decomposition of $R$ into $D = \lbrace R_1, \cdots, R_n \rbrace$.

```
result = alpha
REPEAT
  FOR EACH R[i] IN D
    t = CLOSURE(result INTERSECT R[i]) INTERSECT R[i]
    result = result UNION t
UNTIL (result CONVERGE)
```
If `result` contains all attributes in $\beta$, then the functional dependency $\alpha \to \beta$ is presereved.

This method takes polynomial time, instead of exponential time required when using the definition directly.