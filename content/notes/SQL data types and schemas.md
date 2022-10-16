---
title: "SQL data types and schemas"
math: true
toc: true
---

## Built-in data types in SQL
In addition to the [[notes/SQL data definition#Domain types in SQL | basic data types]], the SQL standard supports several data types:
- `DATE`
  
  Dates in `YYYY-MM-DD` format
  - e.g., `DATE '2001-11-15'`

- `TIME`
  
  Time of day in hours, minutes, and seconds
  - e.g., `TIME '09:00:30'`, `TIME '09:00:30.75'`

- `TIMESTAMP`
  
  Date plus the time of day
  - e.g., `TIMESTAMP '2001-11-15 09:00:30.75'`

- `INTERVAL`
  
  Period of time
  - e.g., `INTERVAL '1' day`
  - Subtracting a `DATE` / `TIME` / `TIMESTAMP` from another gives an `INTERVAL` value
  - `INTERVAL` values can be added to `DATE` / `TIME` / `TIMESTAMP` values

## Large-object types
Many current-generation database applications need to store attributes that can be large. SQL provides large-object data types for **character data** (`CLOB`) and **binary data** (`BLOB`). Here, 'lob' stands for 'Large OBject.'

When a query returns a large object, a **pointer** is returned, rather than the large object itself.

## User-defined types
SQL provides the notion of **distinct types**. The `CREATE TYPE` clause can be used to define new types.
```sql
CREATE TYPE a AS t FINAL;
```
- `a`: Name of the new type
- `t`: Pre-existing type

Before user-defined types were added to SQL, SQL had similar but subtly different notion of **domain**, which can add [[notes/Integrity constraints | integrity constraints]] to an underlying type.
```sql
CREATE DOMAIN d t
    CONSTRAINT ...
```
- `d`: Name of the new domain
- `t`: Pre-existing type

There are two significant differences between types and domains:
- Domains can have constraints specified on them, and can have default values defined for variables of the domain type, whereas user defined types cannot have constraints of default values specified on them.
- Domains are not strongly typed.

## Index creation
Many queries reference only a small proportion of the records in a table. Thus, it is inefficient for the system to read every record to find a record with particular value.

An **index** on an attribute of a relation is a data structure that allows the database system to find those tuples in the relation that have a specified value for that efficiently, _without_ scanning through all the tuples of the relation.
```sql
CREATE INDEX i ON r(A_1, ... , A_k)
```
- `i`: Name of the index
- `r`: Relation
- `A_i`: Attributes

**Example**
```sql
CREATE INDEX studentID_idx ON student(ID);

SELECT  *
FROM    student
WHERE   ID = '12345'
```
The above query can be executed by using the index to find the required record, _without_ looking at all records of student.