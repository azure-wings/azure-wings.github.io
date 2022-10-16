---
title: "Views"
math: true
toc: true
---

In some cases, it is not desirable for all users to see the entire [[notes/View of data#Data models | logical model]] (i.e., all the actual [[notes/Structure of relational databases | relations]] stored in the database).

Aside from security concerns, one may wish to create personalised collection of relations that is better matched to a certain user's intuition than is the logical model.

SQL allows a **virtual relation** to be defined by a query, and the relation conceptually contains the result of the query.

Any such relation that is not part of the logical model, but is made visible to a user as a virtual relation, is called a **view**.

## View definition
A view is defined using the `CREATE VIEW` statement.
```sql
CREATE VIEW v AS Q
```
- `v`: The name of the view
- `Q`: Any legal SQL expression

Once a view is defined, the view name can be used to refer to the virtual relation that the view generates.

View denition is **not** the same as creating a new relation by evaluating the query expression. Rather, a view definition causes the _saving of an expression_; the expression is substituted into queries using the view.

**Examples**
- A view of instructors without their salary
```sql
CREATE VIEW faculty AS
    SELECT  ID,
            name,
            dept_name
    FROM    instructor;
```
- Find all instructors in the Biology department
```sql
SELECT  name
FROM    faculty
-- Views can be used like relations
WHERE   dept_name = 'Biology';
```
- A view of department salary totals
```sql
CREATE VIEW 
    dept_total_salary
    (
        dept_name,
        total_salary
    ) AS
    SELECT  dept_name,
            SUM(salary)
    FROM    instructor
    GROUP BY dept_name;
```

### Views defined using other views
A view can be used in the expression defining another view.

- **Direct dependency**
  
  A view relation $v_1$ is said to **depend directly** on a view relation $v_2$, if $v_2$ is used in the expression defining $v_1$.

- **Dependency**

  A view relation $v_1$ is said to **depend** on a view relation $v_2$, if either $v_1$ depends directly to $v_2$, or there exists a path of dependencies from $v_1$ to $v_2$.

- **Recursion**
  
  A view relation $v$ is said to be **recursive** if it depends on itself.

## View expansion
**View expansion** is a way to define the meaning of views defined in terms of other views.

Suppose that a view $v_1$ is defined by an expression $e_1$ that may itself contain uses of view relations.

It follows the following replacement step:
```
REPEAT
    Find any view relation v_i in e_1
    Replace the view relation v_i by the expression defining v_i
UNTIL nomore view relation are present in e_1
```
As long as the view definitions are _not recursive_, the loop will terminate eventually.

## Materialised views
Certain [[notes/Database systems | database systems]] allow view relations to be physically stored, that is, a physical copy of the 'virtual' relation is created when the view is defined.

Such views are called **materialised views**. It is especially efficient for views that are very commonly used.

If relations used in the query are [[notes/Modificatin of the database | updated]], the materialised view reult becomes **out of date**; views must be maintained to date by updating the view whenever the underlying relations are updated.

### Pros and cons of materialised views
|      | Virtual Relation    | Materialisation             |
|------|---------------------|-----------------------------|
| Pros | No updated required | No query rewriting required |
| Cons | Queries must be rewrited every time | Update required whenever the base relations are updated |