---
title: "Assertion"
math: true
toc: true
---

An **assertion** is a predicate expressing a condition that we wish the database to always satisfy.

[[notes/SQL data definition#Domain types in SQL | Domain constraints]] and [[notes/Integrity constraints#Referential integrity | referential integrity constraint]] are special forms of assertions.

```sql
CREATE ASSERTION a CHECK(p);
```
- `a`: Name of the assertion
- `p`: Predicate

When an assertion is created, the system checks it for validity. If the assertion is valid, then any future modification to the database is allowed only if it does not cause assertion violation.