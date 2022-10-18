---
title: "Advanced aggregation features"
math: true
toc: true
---

## Ranking
Finding the position of a value in a larger set is a common operation. In SQL, **ranking** is done by `RANK() OVER` in conjunction with an `ORDER BY` specification.

**Examples**
- Find the rank of each student
```sql
SELECT  ID,
        RANK() OVER (ORDER BY (GPA) DESC) AS s_rank
FROM    student_grades;
/* student_grades(ID, GPA) is a relation 
 * giving the GPA of each student */
```
Here, an extra `ORDER BY` clause can return the results in sorted order.
```sql
SELECT  ID,
        RANK() OVER (ORDER BY (GPA) DESC) AS s_rank
FROM    student_grades
ORDER BY s_rank ASC;
```

A basic issue with ranking is how to deal with the case of mutiple tuples that are the same values on the ordering attribute(s).

- Naturally, the `RANK()` function leaves gaps.
  
  Meaning that if the highest GPA is shared by two students, both would get rank `1`, and the next rank would be `3`.

- There is a `DENSE_RANK()` function which does not leave gaps.

### Ranking with partitions
Ranking can be done within partitions of data, using `PARTITION BY`.

**Example**
- Find the rank of students within each department
```sql
SELECT  ID,
        dept_name,
        RANK() OVER 
        (
            PARTITION BY dept_name
            ORDER BY GPA DESC
        ) AS dept_rank
FROM    dept_grades
ORDER BY dept_name, dept_rank;
```

- Multiple rank expressions can be used within a single `SELECT` statement.

- When ranking (possibly with partitioning) occurs along with a `GROUP BY` clause, the `GROUP BY` clause is applied first, and partitioning and ranking are done on the results of `GROUP BY`, allowing aggregate values to be used for ranking.

### Other ranking related features
- `PERCENT_RANK`: Gives the rank of the tuple as a fraction
- `CUME_DIST`: Cumulative distribution
- `ROW_NUMBER`: Sorts the rows and gives each row a unique number corresponding to its position
  - Non-deterministic in presence of duplicates

- `NULLS FIRST`, `NULLS LAST`
- `NTILE(n)`: Takes the tuples in each partition in the specified order, and divides them into `n` buckets with **equal numbers of tuples**
  
**Example**
- Find for each student the quartile they belong to
```sql
SELECT  ID,
        NTILE(4) OVER (ORDER BY GPA DESC) AS quartile
FROM    student_grades;
```

## Windowing
Window queries compute an aggregate function over ranges of tuples. They are used to **smooth out** random variables.

Unlike partitions, windows may overlap, in which case a tuple may contribute to more than one window.

SQL provides a windowing feature to support such queries.
```sql
ROWS n_1 PRECEDING AND n_2 FOLLOWING
```

**Example**
- Compute the sum for each three days window.
```sql
SELECT  date,
        SUM(value) OVER
        (
            ORDER BY date
            ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING
        )
FROM    sales;
```

### Other windowing related features
- `UNBOUNDED`: The number of preceding / following rows are unbounded
- `CURRENT ROW`: Specifies the current row
  - e.g., `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`
- `RANGE BETWEEN ...`: Cover all tuples with a particular **value** rather than covering a specific number of tuples

### Windowing with partitions
SQL supports windowing within partitions.

**Example**
- Find total balance of each account after each transaction on the account
```sql
SELECT  account_number,
        date_time,
        SUM(value) OVER
        (
            PARTITION BY account_number
            ORDER BY date_time
            ROWS UNBOUNDED PRECEDING
        ) AS balance
FROM    transaction
ORDER BY account_number, date_time;
```