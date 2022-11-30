---
title: "Database normalisation"
math: true
toc: true
---

The method for designing a relational database is to use a process commonly known as **normalisation**. The goal of database normalisation is to:
- Decide if a given relation schema is in 'good form'.
- If a given relation schema is not in 'good form', losslessly decompose it into a number of smaller relation schemas, each of which is in an appropriate good form.

Database normalisation theory is based on **[[notes/Functional dependency|functional dependencies]]** and **[[notes/Multivalued dependency|multivalued dependencies]]**.

## Notational conventions

- Greek letters $(\alpha, \beta, \cdots)$ are used for attributes.
- $K$ denotes a set of attributes which is a superkey.
- Lowercase names $(r, s, \cdots)$ are used for relations. Uppercase names $(R, S, \cdots)$ are used for relation schemas.
  - $r(R)$ denotes the relation $r$ with schema $R$.