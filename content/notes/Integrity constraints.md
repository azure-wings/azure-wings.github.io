---
title: "Integrity constraints"
math: true
toc: true
---

**Integrity constrains** ensure that changes made to the database by authorised users do not result in a loss of data consistency. Thus, integrity constraints guard against accidental damage to the database.

## Constraints on a single relation
There are some integrity-constraint statements allowed to be included in the `CREATE TABLE` command:
- `NOT NULL`
- `PRIMARY KEY`
- `UNIQUE`
- `CHECK(<predicate>)`

### `NOT NULL` constraint
The [[notes/Null values in SQL | `NULL` value]] is a member of all domains, hence is a legal value for every attribute in SQL by default.

However, for certain attributes, `NULL` values may be inappropriate.

The `NOT NULL` specification prohibits the insertion of a `NULL` value for the attribute.
```sql
A D NOT NULL
```
- `A`: Attribute
- `D`: Domain

### `UNIQUE` constraint
The `UNIQUE` specification states that the attributes specified form a candidate key.
```sql
UNIQUE(A_1, ... , A_n)
```
- `A_i`: Attributes

Attributes $(A_1, \cdots, A_n)$ form a candidate key; that is, no two tuples can be equal on all the listed attributes.

Candidates keys are permitted to be `NULL` (unless explicitly declared to be `NOT NULL`), in contrast to primary keys.

### `CHECK` clause
The `CHECK` clause specifies a predicate `P` that **must** be satisfied by every tuple in a relation.

**Example**
- Ensure that `semester` is one of 'Autumn', 'Winter', 'Spring', or 'Summer'
```sql
CREATE TABLE section
(
    ...
    semester    VARCHAR(6),
    ...
    CHECK(semester IN ('Autumn', 'Winter', 'Spring', 'Summer'))
)
```

### Complex `CHECK` conditions
The predicate in the `CHECK` clause can be an arbitrary predicate that can include a subquery.

**Example**
```sql
CHECK
(
    time_slot_id IN
    (
        SELECT  time_slot_id
        FROM    time_slot
    )
)
```
The condition must be checked not only when a tuple is inserted or modified in `section`, but also the relation `time_slot` changes.

## Referential integrity
**[[notes/SQL data definition#Integrity Constraints | Referential integrity]]** ensures that a value that appears in one relation for a given set of attributes also appears for a certain set of attributes in another relation.

By default, a foreign key references the primary key attributes of the referenced table. Non-primary keys can also be referenced by foreign keys, but the attribute **must** have `UNIQUE` constraint specified.

SQL allows a list of attributes of the referenced relation to be specified explicitly:
```sql
FOREIGN KEY(A_1, ... , A_k) REFERENCES r(B_1, ... , B_k)
```
- `A_i`, `B_i`: Attributes
- `r`: Referenced relation

### Cascading actions in referential integrity
When a referential integrity constraint is violated, the normal procedure is to reject the action that caused the violation. An alternative in case of `DELETE` or `UPDATE` is to **cascade** actions.

`CASCADE` specification ensures that whenever a referenced key is deleted or updated (depending on the specification), the same operation is _cascaded_ to all the referencing keys.

**Example**
```sql
CREATE TABLE course
(
    ...
    dept_name   VARCHAR(20),
    FOREIGN KEY (dept_name) REFERENCES department
        ON DELETE CASCADE
        ON UPDATE CASCADE
);
```
If a `DELETE` of a tuple in `department` results in this reference integrity constraint being violated, the `DELETE` operation _cascades_ to the `course` relation, deleting the tuple that refers to the department that was deleted. Similar process also happens for `UPDATE`.

The followings can be used instead of `CASCADE`:
- `SET NULL`
  
  Whenever a tuple of referenced key relation is removed, set the value of **all** tuples of the referencing key with the same value to `NULL`

- `SET DEFAULT`
  
  Same as above, but use default value instead of `NULL`

- `NO ACTION`
  
  No action is done; referential integrity is violated.

## Integrity constraint violation during a transaction
Integrity constraints may be violated temporarily during [[notes/Transactions | transactions]].

**Example**
```sql
CREATE TABLE person
(
    ID      CHAR(10),
    name    VARCHAR(40),
    mother  CHAR(10),
    father  CHAR(10),
    PRIMARY KEY (ID),
    FOREIGN KEY (father) REFERENCES person,
    FOREIGN KEY (mother) REFERENCES person
);
```
How can a tuple be inserted without causing constraint violation?
There are some ways to do this:
- Insert `father` and `mother` of a person before inserting that person
  
- Set `father` and `mother` to `NULL` initially, and update after inserting all persons
  - Not possible if `father` and `mother` attributes are declared to be `NOT NULL`
  
- Defer constraint checking until the end of the transaction