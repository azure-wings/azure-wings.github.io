---
title: "Modification of the database"
math: true
toc: true
---

## Deletion
A delete request can only delete whole tuples; deleting values on only particular attributes is not allowed.
```sql
DELETE FROM r
WHERE       p
```
- `r`: Relation
- `p`: Predicate

The `DELETE` statement first finds all tuples `t` in `r` for which `P(t)` is true, and then deletes them from `r`.\
Note that `DELETE` command operates on only one relation.

**Examples**
- Delete all tuples from `instructor` table
```sql
DELETE FROM instructor;
```
- Delete all tuples in the instructor relation for those instructors associated with a department located in the Watson building
```sql
DELETE FROM instructor
WHERE       dept_name IN
(
    SELECT  dept_name
    FROM    department
    WHERE   building = 'Watson'
);
```
- Delete all instructors whose salary is less than the average salary of all instructors
```sql
DELETE FROM instructor
WHERE       salary <
(
    SELECT  AVG(salary)
    FROM    instructor
);
```
SQL first computes the average salary and find all tuples to delete, then delete all corresponding tuples from the relation (**without** recomputing or retesting the tuples).

## Insertion
To insert data into a relation, either a tuple to be inserted, or the query whose result is a set of tuples to be inserted, must be specified.
```sql
INSERT INTO r
```
- `r`: Relation

**Examples**
- Insert a new tuple to `course`
```sql

```