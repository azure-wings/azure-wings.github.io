---
title: "Set operations in SQL"
math: true
toc: true
---

## `UNION` Operation

The SQL operation `UNION` corresponds to the mathematical operation $\cup$.

```sql
R1 UNION R2
```

The `UNION` operation automatically **eliminates duplicates**.

To retain duplicates, one must use `UNION ALL` operation instead.

## `INTERSECT` Operation

The SQL operation `INTERSECT` corresponds to the mathematical operation $\cap$.

```sql
R1 INTERSECT R2
```

The `INTERSECT` operation automatically **eliminates duplicates**.

To retain duplicates, one must use `INTERSECT ALL` operation instead.

## `EXCEPT` Operation

The SQL operation `EXCEPT` corresponds to the mathematical operation $\setminus$.

```sql
R1 EXCEPT R2
```

The `EXCEPT` operation outputs all tuples from `R1` that do not occur in `R2`.

The `EXCEPT` operation automatically **eliminates duplicates**.

To retain duplicates, one must use `EXCEPT ALL` operation instead.