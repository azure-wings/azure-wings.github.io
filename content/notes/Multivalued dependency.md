---
title: "Multivalued dependency"
math: true
toc: true
---

[[notes/Functional dependency|Functional dependencies]] rule out certain tuples from being in a relation. **Multivalued dependency**, however, do not rule out the existence of certain tuples; instead, they require that other tuples of a certain form be _present_ in the relation.

## Definition

Let $R$ be a relation schema and let $\alpha, \beta \subseteq R$.

The **multivalued dependency** $\alpha \twoheadrightarrow \beta$ ($\alpha$ **multidetermines** $\beta$) holds on $R$ if in any legal relation $r(R)$, for all pairs of tuples $t_1, t_2 \in R$ such that $t_1[\alpha] = t_2[\alpha]$, there exists tuples $t_3, t_4 \in R$ that satisfies all of the followings:
- $t_1[\alpha] = t_2[\alpha] = t_3[\alpha] = t_4[\alpha]$
- $t_3[\beta] = t_1[\beta]$
- $t_3[R \setminus \beta] = t_2[R \setminus \beta]$
- $t_4[\beta] = t_2[\beta]$
- $t_4[R \setminus \beta] = t_1[R \setminus \beta]$

The following is a tabular representation of the multivalued dependency $\alpha \twoheadrightarrow \beta$.

|       | $\alpha$ | $\beta$ | $R \setminus (\alpha \cup \beta)$ |
|-------|----------|---------|-----------------------------------|
| $t_1$ | E | A | C |
| $t_2$ | E | B | C |
| $t_3$ | E | A | D |
| $t_4$ | E | B | D |

### Alternate definition

Let $R$ be a relation schema with a set of attributes that are partitioned into 3 nonempty subsets $X, Y, Z$.

Then, $X \twoheadrightarrow Y$ holds on $R$ if and only if for all possible relations $r(R)$:
$$
\begin{align*}
\langle x_1, y_1, z_1 \rangle, \langle x_1, y_2, z_2 \rangle \in r \\ \Rightarrow \langle x_1, y_1, z_2 \rangle, \langle x_1, y_2, z_1 \rangle \in r
\end{align*}
$$

Note that since the behaviour of $Y$ and $Z$ are identical, it follows that $X \twoheadrightarrow Y \Leftrightarrow X \twoheadrightarrow Z$.

## Use of multivalued dependencies

Multivalued dependencies can be used to:
- Test relations to determine whether they are legal under a given set of functional and multivalued dependencies.
- Specify constraints on the set of legal relations.

If a relation $r$ fails to satisfy a given multivalued dependency, a relation $r'$ that satisfies the multivalued dependency can be constructed by adding additional tuples to $r$.