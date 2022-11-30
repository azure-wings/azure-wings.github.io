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