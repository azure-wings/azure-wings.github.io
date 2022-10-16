---
title: "Integrity constraints"
math: true
toc: true
---

**Integrity constrains** ensure that changes made to the database by authorised users do not result in a loss of data consistency. Thus, integrity constraints guard against acciendtal damage to the database.

## Constraints on a single relation
There are some integrity-constraint statements allowe to be included in the `CREATE TABLE` command:
- `NOT NULL`
- [[notes/SQL data definition#Integrity Constraints | `PRIMARY KEY`]]
- `UNIQUE`
- `CHECK(<predicate>)`

### `NOT NULL` constraint
The [[notes/Null values in SQL | `NULL` value]] is a member of all domains, hence is a legal value for every attribute in SQL by default.

However, for certain attributes, `NULL` values may be inappropriate.

The `NOT NULL` specification prohibits the insertion of a `NULL` value for the attribute.
```sql
A D NOT NULL
```
- `A`: Attribute
- `D`: Domain

### `UNIQUE` constraint
The `UNIQUE` specification states that the attributes specified form a candidate key.
```sql
UNIQUE(A_1, ... , A_n)
```
- `A_i`: Attributes

Attributes $(A_1, \cdots, A_n)$ form a candidate key; that is, no two tuples can be equal on all the listed attributes.

Candidates keys are permitted to be `NULL` (unless explicitly declared to be `NOT NULL`), in contrast to primary keys.

### `CHECK` clause
The `CHECK` clause specifies a predicate `P` that **must** be satisfied by every tuple in a relation.

**Example**
- Ensure that `semester` is one of 'Autumn', 'Winter', 'Spring', or 'Summer'
```sql
CREATE TABLE section
(
    ...
    semester    VARCHAR(6),
    ...
    CHECK(semester IN ('Autumn', 'Winter', 'Spring', 'Summer'))
)
```

## Referential integrity
