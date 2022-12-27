---
title: "Restriction(Database)"
math: true
toc: true
---

## Definition

### Functional dependency

Let $F$ be the set of [[notes/Functional dependency|functional dependencies]] on schema $R$, and let $R_1, \cdots, R_n$ be a decomposition of $R$.

The **restriction** of $F$ to $R_i$, denoted as $F_i$, is the set of all functional dependencies in the **[[notes/Closure(Database)#Closure of functional dependencies|closure]]** $F^+$ (Note: **not** $F$) that include only attributes of $R_i$.

### Multivalued dependency

Let $D$ be the set of functional and [[notes/Multivalued dependency|multivalued dependencies]] on schema $R$, and let $R_1, \cdots, R_n$ be a decomposition of $R$.

The **restriction** of $D$ to $R_i$, denoted as $D_i$, is the set of all functional and multivalued dependencies in the **[[notes/Closure(Database)#Closure of multivalued dependencies|closure]]** $D^+$ that include only attributes of $R_i$.

That is,
- All functional dependencies in $D^+$ that include only attributes of $R_i$.
- All multivalued dependencies of the form $\alpha \twoheadrightarrow (\beta \cap R_i)$, where $\alpha \subseteq R_i$ and $\alpha \twoheadrightarrow \beta \in D^+$.