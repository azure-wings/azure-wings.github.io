---
title: "Join expressions"
math: true
toc: true
---

## Natural join
The **natural join** operation operates on two relations and produces a relation as a result.

It matches tuples with the same values for **all common attributes**, and retains only one copy of each common attribute.
```sql
r_1 NATURAL JOIN r_2
```
Unlike the Cartesian product of two relations, natural join considers only those pairs of tuples with the same value on those attributes that appear on the schema of both relations.

It is an **equi-join** which occurs **implicitly** by comparing all the same name columns in both relations.

## Join conditions
To prevent equating attributes erroneously, SQL supports the specification of the join condition.

### `USING` construct
The operation `JOIN ... USING` requires a list of attribute names to be specified.
```sql
r_1 JOIN r_2 USING(A_1, ... , A_n)
```
- `r_i`: Relation
- `A_i`: Attribute

The operation is equivalent to:
```sql
SELECT  *
FROM    r_1,
        r_2
WHERE   r_1.A_1 = r_2.A_1
AND     ...
AND     r_1.A_n = r_2.A_n
```
It is an **equi-join**, and causes duplicate attributes to be **removed** from the resultset.

### `ON` construct
The `ON` condition allows a general predicate over the relaions being joined.

This predicate is written like a `WHERE` clause predicate.
```sql
r_1 JOIN r_2 ON p
```
- `r_i`: Relation
- `p`: Predicate
The operation is equivalent to:
```sql
SELECT  *
FROM    r_1,
        r_2
WHERE   p
```
It is a **theta join**, and it allows duplicate attributes to appear in the resultset.

**Example**
- All attributes about all students, along with all the courses that they have took
```sql
SELECT  *
FROM    student
JOIN    takes
ON      student.ID = takes.ID
```
- Note that the above query has **two** occurrences for the attribute `ID`, and the relation name of origin must be specified to disambiguate the two.

#### Comparison of `ON` and `USING`
In a nutshell, `ON` can be used for most joins, but `USING` is a handy shorthand for the situation where _the column names are the same_.

The following queries are equivalent.
```sql
SELECT  I.title, R.name
FROM    albums I
INNER JOIN  artists R
ON      R.artist_id = I.artist_id;
```
```sql
SELECT  title, name
FROM    albums
INNER JOIN  artists
USING(artist_id);
```

## Outer join
The **outer join** is an extension of the join operation that **avoids loss of information**.

It computes the join operation, and then adds tuples from one relation that does not match tuples in the other relation to the result of the join, using `NULL` values.

There are three forms of outer join:
- **`LEFT OUTER JOIN`**

  Preserves tuples only in the relation named to the left of the `LEFT OUTER JOIN` operation.
- **`RIGHT OUTER JOIN`**
  
  Preserves tuples only in the relation named to the right of the `RIGHT OUTER JOIN` operation.
- **`FULL OUTER JOIN`**
  
  Preserves tuples in both relations.

![sql-join-visualisation](/notes/images/sql-join-visualisation.png)

In constrast, the join operations that do not preserve nonmatched tuples are called `INNER JOIN` operations.