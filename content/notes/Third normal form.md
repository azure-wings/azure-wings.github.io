---
title: "Third normal form"
math: true
toc: true
---

## Definition

A relation schema $R$ is in **third normal form(3NF)** with respect to a set of [[notes/Functional dependency|functional dependencies]] $F$ if:

For all functional dependencies $\alpha \to \beta \in F^+$, where $\alpha, \beta \subseteq R$, at least one of the following holds:
- $\alpha \to \beta$ is trivial. (i.e., $\beta \subseteq \alpha$)
- $\alpha$ is a [[notes/Keys|superkey]] of $R$. (i.e., $\alpha \to R$)
- Each attribute $A$ in $\beta \setminus \alpha$ is contained in a candidate key for $R$.
  - Note that each attribute may be in a different candidate key.

If a relation is in [[notes/Boyce-Codd normal form|BCNF]], then it is in 3NF also. The third condition is a minimal relaxation to BCNF to ensure **[[notes/Dependency preservation|dependency preservation]]**.

Note that for any relation schema, there **always** exists a lossless, dependency preserving decomposition into 3NF.

### Example

Consider a schema $R = \texttt{dept-advisor}(\texttt{sID}, \texttt{iID}, \texttt{deptName})$ with the functional dependencies $\texttt{iID} \to \texttt{deptName}$ and $\texttt{sID}, \texttt{deptName} \to \texttt{iID}$.

Then, the candidate keys are $\lbrace \texttt{sID}, \texttt{deptName} \rbrace$ and $\lbrace \texttt{sID}, \texttt{iID} \rbrace$.

Although $R$ is not in BCNF, $R$ is in 3NF.

## Testing for 3NF

Unlike [[notes/Boyce-Codd normal form#Testing for BCNF|testing for BCNF]], testing for 2NF need not check all functional dependencies in $F^+$; it only requires to check only functional dependencies in $F$ itself.

Let $R$ be a relation schema, and let $F$ be the set of functional dependencies.

1. For every functional dependency $\alpha \to \beta \in F$, compute $\alpha^+$.
2. If $\alpha \to R$, $\alpha \to \beta$ does not violate 3NF.
3. Otherwise if $\alpha$ is not a superkey of $R$, verify if each attribute in $\beta$ is contained in a candidate key of $R$.

This test is rather more expensive, since it involves finding candidate keys. This test is shown to be NP-hard.

## Decomposition into 3NF

![3nf-decompose-algorithm](notes/images/3nf-decompose-algorithm.png)

The above algorithm ensures that:
- Each relation schema $R_i$ is in 3NF.
- Decomposition is dependency preserving and lossless.