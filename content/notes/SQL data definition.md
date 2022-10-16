---
title: "SQL data definition"
math: true
toc: true
---

## Domain types in SQL

- **`CHAR(n)`**
  
    Fixed-length character string, with user-specified length `n`
    
- **`VARCHAR(n)`**
  
    Variable-length character string, with user-specified **maximum** length `n`
    
- **`INT`**
  
    Integer (machine-dependent)
    
- **`SMALLINT`**
  
    Small integer (machine-dependent)
    
- **`NUMERIC(p, d)`**
  
    Fixed-point  number, with user-specified precision of `p` digits (plus a sign), with `d` digits to the right of the decimal point
    - `NUMERIC(3, 1)` allows `44.5` to be stored exactly, but neither `444.5` or `0.32` can be stored exactly.
  
- **`REAL`, `DOUBLE PRECISION`**
  
    Floating-point and double precision floating-point numbers (machine-dependent precision)
    
- **`FLOAT(n)`**
  
    Floating-point number, with user-specified precision of at least `n` digits
    

## Basic schema definition

An SQL relation is defined using the `CREATE TABLE` command.

```sql
CREATE TABLE r
(
	A_1 D_1,
	... ,
	A_n D_n,
	[Integrity Constraint 1],
	... ,
	[Integrity Constraint k]
)
```

- `r`: Name of the relation
- `A_i`: Attribute name in the schema of the relation `r`
- `D_i`: Data type of values in the domain of attribute `A_i`

**Example**
```sql
CREATE TABLE instructor
(
	ID           CHAR(5),
	name         VARCHAR(20) NOT NULL,
	dept_name    VARCHAR(20),
	salary       NUMERIC(8, 2),
	PRIMARY KEY(ID),
	FOREIGN KEY(dept_name) REFERENCES department
);
```
    

### Integrity Constraints

- **`PRIMARY KEY(A_1, ... , A_n)`**
    - Attributes `A_1`, … , `A_n` form the primary key for the relation.
    - Required to be *non-null* and *unique*.
    
- **`FOREIGN KEY(A_1, ... , A_n) REFERENCES s`**
    - Values of attributes `(A_1, ... , A_n)` for any tuple in the relation *must* correspond to values of the **primary key** attributes (or any attributes with `UNIQUE` constraint specified) of some tuple in relation `s`
    
- **`NOT NULL`**
    - `NULL` value is not allowed for that attribute
    

### Updates to Tables

- **`INSERT INTO s t`**
    - Inserts tuple `t` into the relation `s`
    - e.g., `INSERT INTO instructor VALUES('10211', 'Smith', 'Biology', 66000)`

- **`DELETE FROM s t`**
    - Deletes tuple `t` from the relation `r`
    - e.g., `DELETE FROM student` deletes **all** tuples from the relation `student`
    
- **`DROP TABLE r`**
    - Deletes all information of `r`, including the table itself, from the database
    - After `r` is dropped, no tuples can be inserted into it unless it is re-created with the `CREATE TABLE` command
    
- **`ALTER`**
    - **`ALTER TABLE r ADD A D`**\
        `A` is the name of the attribute to be added to relation `r`, and `D` is the domain of `A`
        
        All existing tuples in the relation are assigned `NULL` as the value for the new attribute
        
    - **`ALTER TABLE r DROP A`**\
        `A` is the name of an attribute of relation `r`