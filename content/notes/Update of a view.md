---
title: "Update of a view"
math: true
toc: true
---

Although [[notes/Views | views]] are a useful tool for queries, they present serious problems when undergoing _updates_, _insertions_, or _deletions_.

## Missing attribute
**Example**
- Add a new tuple to the view `faculty` defined earlier
```sql
INSERT INTO faculty VALUES
    ('30765', 'Green', 'Music');
```
This insertion must be represented by the insertion into the `instructor` relation, which must have a `salary` attribute.
There are two reasonable approaches to dealing with this insertion.
- Reject the insertion.
- Insert a tuple with the value of the non-existing attribute set to `NULL`.
  - Will be rejected by the [[notes/Database systems | DBMS]] if that attribute has `NOT NULL` constraint.

## Ambiguity
Another problem with modification of the database through views occurs when updates cannot be **translated uniquely**.

**Examples**
```sql
CREATE VIEW instructor_info AS
    SELECT  ID,
            name,
            building
    FROM    instructor,
            department
    WHERE   instructor.dept_name = department.dept_name

INSERT INTO instructor_info VALUES
    ('69987', 'White', 'Taylor');
```
- Which department, if multiple departments exist in the `Taylor` building, should the value be inserted to?
- What if there is no department in the `Taylor` building?
  
There is no way to update the relations `instructor` and `department` by using `NULL` values to get the desired update on the view `instructor_info`.

Consider another problematic scenario.
```sql
CREATE VIEW history_instructors AS
    SELECT  *
    FROM    instructor
    WHERE   dept_name = 'History'

INSERT INTO history_instructors VALUES
    ('25566', 'Brown', 'Biology', 7000);
```
- Should the insertion be allowed?

## View updates in SQL
Because of problems such as above, modifications are generally **not permitted** on view relations, except in limited cases.

Most SQL implementations allow updates only on simple views:
- The `FROM` clause has only one database relation.
  
- The `SELECT` clause contains only attributes of the relation, and does **not** have any expression, aggregates, or `DISTINCT` specification.
  
- Any attribute not listed in the `SELECT` clause can be set to `NULL`.
  
- The query does not have a `GROUP BY` or `HAVING` clause.