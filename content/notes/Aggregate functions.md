---
title: "Aggregate functions"
math: true
toc: true
---

**Aggregate functions** are functions that take a collection of values as input, and return a single value.

SQL offers five aggregate functions:

- Average: `AVG`
- Minimum: `MIN`
- Maximum: `MAX`
- Total: `SUM`
- Count: `COUNT`

The input to `AVG` and `SUM` must be a collection of numbers.

## Aggregation with Grouping

`GROUP BY` clause uses the given attributes to form groups.

```sql
GROUP BY some_attributes
```

- **Example**
    
    Find the average salary of instructors in each department.
    
    ```sql
    SELECT   dept_name,
    				 AVG(salary) AS avg_salary
    FROM     instructor
    GROUP BY dept_name
    ```
    

Attributes in `SELECT` statement that is outside of aggregate functions **must** appear in the `GROUP BY` clause; otherwise the query is treated as erroneous.

## `HAVING` Clause

SQL applies predicated in the `HAVING` clause **after** the formation of groups, whereas predicates in the `WHERE` clause are applied **before** the group formation.

```sql
GROUP BY some_attributes
HAVING   predicate
```

A typical query containing aggregation, `GROUP BY`, and/or `HAVING` clauses is defined by the following sequence of operations.

1. The `FROM` clause is first  evaluated to get a relation.
2. If a `WHERE` clause is present, the predicate in the `WHERE` clause is applied on the result relation of the `FROM` clause.
3. Tuples satisfying the `WHERE` predicate are then placed into groups by the `GROUP BY` clause (if present).
Otherwise the entire set of tuples satisfying `WHERE` clause’s predicate is treated as one single group.
4. The `HAVING` clause (if present) is applied to **each group**, the groups that do not satisfying the `HAVING` predicate are removed.
5. The `SELECT` clause uses the remaining groups to generate tuples of the result of the query, applying the aggregate functions to get a single result tuple for each group.

## Aggregation with `NULL` Values

- All aggregate functions except `COUNT` ignore `NULL` values in their input collection.
- The `COUNT` of an empty collection is defined to be `0`.
- All other aggregate operations return a value `NULL` when applied to an empty collection.