---
title: "Comparison between BCNF and 3NF"
math: true
toc: true
---

It is always possible to decompose a relation into a set of relations that are in [[notes/Boyce-Codd normal form|BCNF]] such that:

- The decomposition is **[[notes/Overview of normalisation#Lossless decomposition|lossless]]**.

It is always possible to decompose a relation into a set of relations that are in [[notes/Third normal form|3NF]] such that:

- The decomposition is **[[notes/Overview of normalisation#Lossless decomposition|lossless]]**.
- The decomposition **[[notes/Dependency preservation|preserves dependencies]]**.

|    | BCNF | 3NF |
|----|------|-----|
| Redundancy | Less than 3NF | More than BCNF |
| Lossless Decomposition | Always guaranteed | Always guaranteed |
| Dependency Preservation | Not guaranteed | Always guaranteed |