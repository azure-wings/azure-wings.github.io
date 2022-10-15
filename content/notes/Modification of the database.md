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
INSERT INTO course
    VALUES('CS360', 'Introduction to Database', 'SoC', 3)
```
- Make each student in the Music department who has earned more than 144 credit as an instructor in the Music department with a salary of 18000
```sql
INSERT INTO instructor
(
    SELECT  ID,
            name,
            dept_name,
            18000
    FROM    student
    WHERE   dept_name = 'MUSIC'
            AND tot_credit > 144
); 
```
The `SELECT` - `FROM` - `WHERE` statement is **evaluated fully before** any of its results are inserted into the relation.

## Update
A value in a tuple can be changed without changing _all_ values in the tuple with the `UPDATE` statement.
```sql
UPDATE  r
SET     A = (Some Value)
```
- `r`: Relation
- `A`: Attribute

**Examples**
- Give a 5% salary raise to those instructors who earn less than 70000
```sql
UPDATE  instructor
SET     salary = salary * 1.05
WHERE   salary < 70000;
```
- Give a 5% salary raise to instructors whose salary is less than the average of all instructors
```sql
UPDATE  instructor
SET     salary = salary * 1.05
WHERE   salary <
(
    SELECT  AVG(salary)
    FROM    instructor
);
```
Note that the order of `UPDATE` statements is very important.\
Consider the following query.
```sql
-- Update 1
UPDATE  instructor
SET     salary = salary * 1.03
WHERE   salary > 100000
-- Update 2
UPDATE  instructor
SET     salary = salary * 1.05
WHERE   salary <= 100000
```
If the order of the two updates are changed, the results whould not be as desired.\
To prevent order related problems, `CASE` construct is provided by SQL.

### `CASE` construct
`CASE` construct can be used in any place where a value is expected.
```sql
CASE
    WHEN  P_1 THEN  R_1
    ...
    WHEN  P_n THEN  R_n
    ELSE            R_0
END
```
- `P_i`: Predicates
- `R_i`: Resulting value
  
The error-prone query above can be re-written using `CASE` construct.
```sql
UPDATE  instructor
SET     salary =
(
    CASE
        WHEN salary <= 100000 THEN salary * 1.05
        ELSE salary * 1.03
    END
);
```
### Updates with scalar subqueries
Scalar subqueries are also useful in SQL update statements, where they can be used in `SET` clause.

**Example**
- Recompute and update `tot_credit` for all students to the credits of courses successfully completed by the student (successfully completed means `grade` is not `F` nor `NULL`)
```sql
UPDATE  student S
SET     tot_credit =
(
    SELECT  SUM(credits)
    FROM    takes JOIN course USING(course_id)
    WHERE   S.ID = takes.ID AND
            (
                takes.grade <> 'F' AND
                takes.grade IS NOT NULL
            )
);
```