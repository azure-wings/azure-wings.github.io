---
title: "Nested subqueries"
math: true
toc: true
---

A **subquery** is a `SELECT` - `FROM` - `WHERE` expression that is nested within another query.

SQL provides a mechanism for the nesting of subqueries.

## Set Membership

SQL allows testing tuples for membership in a relation, using `IN` or `NOT IN` clause.

- **Examples**
    - Name all instructors whose name is neither “Mozart” nor “Einstein”
    
    ```sql
    SELECT  DISTINCT name
    FROM    instructor
    WHERE   name NOT IN ('Mozart', 'Einsten');
    ```
    
    - Find all the courses taught in the Fall 2009 semester, but not in the Spring 2010 semester
    
    ```sql
    SELECT  DISTINCT course_id
    FROM    section
    WHERE   semester = 'Fall' AND year = 2009 AND course_id NOT IN
    (
    		SELECT  course_id
    		FROM    section
    		WHERE   semester = 'Spring' AND year = 2010
    );
    ```
    
    - Find the total number of distinct students who have taken course sections taught by the instructor with ID `10101`
        - As seen in the example query below, it is possible to test for membership in an arbitrary relation.
    
    ```sql
    SELECT  COUNT(DISTINCT ID)
    FROM    takes
    WHERE   (course_id, sec_id, semester, year) IN
    (
        SELECT  course_id, sec_id, semester, year
    		FROM    teaches
    		WHERE   teaches.ID = 10101
    );
    ```
    

## Set Comparison

### `SOME` Clause

`SOME` clause can check if the predicate is satisfied by at least one tuple in the relation.

- `F <comp> SOME r` $\Leftrightarrow$
$\exists \, t \in r$  such that $(F\;\texttt{<comp>}\; t)$, where $\texttt{<comp>} \in \{<, \leq, >, \geq, =, \neq\}$
- `= SOME` $\Leftrightarrow$ `IN`, however `<> SOME` $\not\Leftrightarrow$ `NOT IN`
- **Example**
    
    Find names of instructors with salary greater than that of some (at least one) instructor in the Biology department
    
    ```sql
    SELECT  DISTINCT T.name
    FROM    instructor AS T,
    				instructor AS S
    WHERE   T.salary > S.salary AND S.dept_name = 'Biology';
    ```
    
    ```sql
    -- Using SOME clause
    SELECT  name
    FROM    instructor
    WHERE   salary > SOME
    (
        SELECT  salary
        FROM    instructor
    		WHERE   dept_name = 'Biology'
    );
    ```
    

### `ALL` Clause

`ALL` clause can check if the predicate is satisfied by all of the tuples in the relation.

- `F <comp> ALL r` $\Leftrightarrow$
$\forall\, t \in r$ such that $(F \;\texttt{<comp>}\; t)$, where  $\texttt{<comp>} \in \{<, \leq, >, \geq, =, \neq\}$
- `<> ALL` $\Leftrightarrow$ `NOT IN`, however `= ALL` $\not\Leftrightarrow$ `IN`
- **Example**
    
    Find the names of all instructors whose salary is greater the salary of all instructors in the Biology department
    
    ```sql
    SELECT  name
    FROM    instructor
    WHERE   salary > ALL
    (
        SELECT  salary
    		FROM    instructor
    		WHERE   dept_name = 'Biology'
    );
    ```
    

## Test for Empty Relations

The `EXISTS` construct returns the value `TRUE` if the argument subquery is nonempty.

- `EXISTS r` $\Leftrightarrow$ $r \neq \emptyset$
- `NOT EXISTS r` $\Leftrightarrow$ $r = \emptyset$
- **Example**
    
    Find all students who have taken all courses offered in the Biology department
    
    ```sql
    SELECT  DISTINCT S.ID,
    		    S.name
    FROM    student AS S
    WHERE   NOT EXISTS
    (
    		SELECT  course_id
    		FROM    course
    		WHERE   dept_name = 'Biology'
    		EXCEPT
    		SELECT  T.course_id
    		FROM    takes AS T
    		WHERE   S.ID = T.ID
    );
    ```
    
    - Note that $X - Y = \emptyset \Leftrightarrow X \subseteq Y$
    - This query **cannot** be written using `= ALL` and its variants

## Test for the Absence of Duplicate Tuples

The `UNIQUE` construct tests whether a subquery has any duplicate tuples in its result.

It evaluates to `TRUE` if a given subquery contains no duplicates.

- **Example**
    
    Find all courses that were offered at most once in 2017
    
    ```sql
    SELECT  T.course_id
    FROM    course AS T
    WHERE   UNIQUE
    (
    		SELECT  R.course_id
    		FROM    course AS R
    		WHERE   T.course_id = R.course_id
    						AND R.year = 2017
    );
    ```
    

## Subqueries in the `FROM` Clause