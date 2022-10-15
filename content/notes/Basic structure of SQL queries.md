---
title: "Basic Structure of SQL Queries"
math: true
toc: true
---

## Basic Query Structure

A typical SQL query has the following form.

```sql
SELECT  A_1, ... , A_n
FROM    r_1, ... , r_m
WHERE   p
```

- `A_i`: Attributes
- `R_i`: Relations
- `P`: Predicate

The result of an SQL query is a relation.

### `SELECT` Clause

- The `SELECT` clause lists the attributes desired in the result of a query.
    
    It corresponds to the projection operation $\Pi$ of the [relational algebra](Relational%20Algebra%20d48d3c6b16584d9f96d66cfc182e0d6f.md).
    
    Note that SQL names are case insensitive.
    
- The `DISTINCT` keyword inserted after `SELECT` eliminates all duplicates.
    
    The `ALL` keyword, on the other hand, explicitly specifies that duplicates should not be removed, although it is the default of `SELECT` clause.
    
- An `*` in the `SELECT` clause denotes all attributes.
- An attribute can be a literal **without** `FROM` clause.
    
    The result is a table with one column and a single row with the literal value.
    
- An attribute can be a literal **with** `FROM` clause.
    
    The result is a table with one column and rows (number equal to the number of rows on the table), each row with the literal value
    
- `SELECT` clause can contain arithmetic expressions (`+`, `-`, `*`, `/`) operating on constants or attributes of tuples.

### `FROM` Clause

- The `FROM` clause lists the relations involved in the query.
    
    It corresponds to the Cartesian product $\times$ of the relational algebra.
    

### `WHERE` Clause

- The `WHERE` clause specifies conditions that the resulting relation must satisfy.
    
    It corresponds to the selection predicate $\sigma$ of the relational algebra.
    
- SQL allows the use of the logical connectives `AND`, `OR`, and `NOT`.
- The operands of the logical connectives can be expressions involving the comparison operators, `<`, `<=`, `>`, `>=`, `=`, and `<>`.
    
    Comparisons can be applied to results of arithmetic expressions.