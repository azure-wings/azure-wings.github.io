---
title: "Fourth normal form"
math: true
toc: true
---

## Definition

Let $R$ be a relation schema, and $D$ be a set of [[notes/Functional dependency|functional]] and [[notes/Multivalued dependency|multivalued dependencies]] of $R$. Let $D^+$ be the [[notes/Closure(Database)#Closure of multivalued dependencies|closure]] of $D$.

Then, $R$ is said to be in **fourth normal form(4NF)** if, for all multivalued dependencies $\alpha \twoheadrightarrow \beta \in D^+$, at least one of the followings hold:
- $\alpha \twoheadrightarrow \beta$ is trivial. (i.e., $\beta \subseteq \alpha$, or $\alpha \cup \beta = R$)
- $\alpha$ is a [[notes/Keys|superkey]] of $R$. (i.e., $\alpha \to R$)

## Decomposition into 4NF

![4nf-decompose-algorithm](notes/images/4nf-decompose-algorithm.png)