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

If a relation is in [[notes/Boyce-Codd normal form|BCNF]], then it is in 3NF also. The third condition is a minimal relaxation to BCNF to ensure [[notes/Functional dependency#Dependency preservation|dependency preservation]].

## Example

Consider a schema $R = \texttt{dept-advisor}(\texttt{sID}, \texttt{iID}, \texttt{deptName})$ with the functional dependencies $\texttt{iID} \to \texttt{deptName}$ and $\texttt{sID}, \texttt{deptName} \to \texttt{iID}$.

Then, the candidate keys are $\{ \texttt{sID}, \texttt{deptName} \}$ and $\{ \texttt{sID}, \texttt{iID} \}$.

Although $R$ is not in BCNF, $R$ is in 3NF.