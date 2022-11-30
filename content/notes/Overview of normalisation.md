---
title: "Overview of normalisation"
math: true
toc: true
---

Suppose that the tables `instructor` and `department` are combined via [[notes/Join expressions#Natural join|natural join]].

![bad-relation-design-example](notes/images/bad-relation-design-example.png)

This relation design is not good because:
- There are repetitions of information.
- [[notes/Null values in SQL|Null values]] must be used when a new `department` with no `instructor` is added.

However, not all combined schemas result in repetitions of information.

## Decomposition

The only way to avoid the repetition-of-information problem in the previous example is to **decompose** it into two schemas: `instructor` and `department`.

However, not all decompositions are good. Consider the decomposition
| Relation | Attributes |
| -------- | ---------- |
| employee | ID, name, street, city, salary |

into

| Relation | Attributes |
| -------- | ---------- |
| employee1 | ID, name |
| employee2 | name, street, city, salary |

The problem arises when there are multiple employees with the same name.

![lossy-decomposition-example](notes/images/lossy-decomposition-example.png)

Such decomposition is unable to represent certain important facts about the relation before the decomposition. This kind of decomposition is referred to as a **lossy decomposition**. Conversely, those that are not are referred to as **lossless decomposition**.

## Lossless decomposition
Let $r$ be a relation, $R$ be a relation schema of $r$ and let $R_1, R_2$ form a decomposition of $R$. In other words, $R = R_1 \cup R_2$.

The decomposition is said to be **lossless** if there is no loss of information by replacing $R$ with $R_1 \cup R_2$. Or equivalently,

$$
\Pi_{R_1}(r) \bowtie \Pi_{R_2}(r) = r
$$

Conversely, a decomposition is said to be **lossy** if

$$
r \subsetneq \Pi_{R_1}(r) \bowtie \Pi_{R_2}(r)
$$

### Definitions with functional dependencies

[[notes/Functional dependency|Functional dependencies]] can be used to show when certain decompositions are lossless.

Consider the decomposition of $R$ into $R_1, R_2$. The sufficient condtion for it to be a **lossless decomposition** is that _at least one_ of the following dependencies is in $F^+$:
- $R_1 \cap R_2 \to R_1$
- $R_1 \cap R_2 \to R_2$