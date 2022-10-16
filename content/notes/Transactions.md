---
title: "Transactions"
math: true
toc: true
---

A **transaction** consists of a sequence of query and/or update statements. It is a 'unit' of work.

The SQL standard specifies that a transaction begins implicitly when an SQL statement is executed.

The transaction must end with one of the following statements:
- **Commit work**
  
  The updates performed by the transaction become permanent in the database.

- **Rollback work**
  
  **All** the updates performed by the SQL statements in the transaction are undone.

The database provides an abstraction of a transaction as being [[notes/Atomic operation | atomic]], that is, indivisible. Either **all** the effects of the transaction are reflected in the database, or **none** are (after rollback).
