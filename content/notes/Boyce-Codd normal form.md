---
title: "Boyce-Codd normal form"
math: true
toc: true
---

## Definition

A relation schema $R$ is in **Boyce-Codd normal form(BCNF)** with respect to a set of [[notes/Functional dependency|functional dependencies]] $F$ if:

For all functional dependencies $\alpha \to \beta \in F^+$, where $\alpha, \beta \subseteq R$, at least one of the following holds:
- $\alpha \to \beta$ is trivial. (i.e., $\beta \subseteq \alpha$)
- $\alpha$ is a [[notes/Keys|superkey]] of $R$. (i.e., $\alpha \to R$)

### Example

Consider $\texttt{in-dep(\underline{ID}, name, salary, \underline{deptName}, building, budget)}$, and the set of functional dependencies $F = \lbrace \texttt{ID} \to \lbrace \texttt{name,deptName,salary} \rbrace, \texttt{deptName} \to \lbrace \texttt{building,budget} \rbrace \rbrace$.
  - This is **not** in BCNF because
    - $\texttt{deptName} \to \texttt{building,budget}$ holds in $\texttt{in-dep}$, but
    - $\texttt{deptName}$ is **not** a superkey.

## Testing for BCNF

### Testing a functional dependency

To check if a nontrivial functional dependency $\alpha \to \beta$ causes a violation of BCNF:

1. Compute $\alpha^+$.
2. Verify that $R \subseteq \alpha^+$. i.e., $\alpha^+$ is a superkey of $R$.

### Testing a relation schema decomposition

Let $R$ be a relation schema, and $R_1, \cdots, R_n$ be a decomposition of $R$. Let $F$ be the set of functional dependencies.

1. For every set of attributes $\alpha \subseteq R_i$, compute $\alpha^+$. 
2. Verify that either $\alpha^+ \cap (R_i \setminus \alpha) = \empty$ or $R \subseteq \alpha^+$.
   - If the condition is violated by some $\alpha$, the dependency $\alpha \to \left( (\alpha^+ \setminus \alpha) \cap R_i \right) \in F^+$. Hence $R_i$ violates BCNF.

## Decomposition into BCNF

Let $R$ be a schema that is not in BCNF, and let $\alpha \to \beta$ be the functional dependency that causes a violation in BCNF.

Then, the following decomposition of $R$ is in BCNF.
- $\alpha \cup \beta$
- $R \setminus (\beta \setminus \alpha)$

In most cases, $\beta \setminus \alpha = \beta$.

### Example
Consider a schema $R = \texttt{dept-advisor}(\texttt{\underline{sID}}, \texttt{\underline{deptName}}, \texttt{iID})$ with the functional dependencies $\texttt{iID} \to \texttt{deptName}$ and $\texttt{sID}, \texttt{deptName} \to \texttt{iID}$.

Here, the dependency $\texttt{iID} \to \texttt{deptName}$ is causing a violation of BCNF conditions.

The decomposition
- $\alpha \cup \beta = (\texttt{iID}, \texttt{deptName})$
- $R \setminus (\beta \setminus \alpha) = (\texttt{sID}, \texttt{iID})$

is in BCNF.

However, any of the decomposed relation does not include all the attributes used in the dependency $\texttt{sID}, \texttt{deptName} \to \texttt{iID}$; it is **not** dependency preserving.