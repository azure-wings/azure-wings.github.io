---
title: "Null values in SQL"
math: true
toc: true
---

**`NULL` values** signifies an unknown value or that a value does not exist.

## Arithmetic operations

The result of **any** arithmetic expression involving `NULL` is `NULL`.

## Comparison operations

SQL treats as `UNKNOWN` the result of **any** comparison involving a `NULL` value, other than `IS NULL` and `IS NOT NULL`.

The predicate in a `WHERE` clause can involve Boolean operations such as `AND`, `OR`, and `NOT`.

- **`AND`**
    - `TRUE AND UNKNOWN` = `UNKNOWN`
    - `FALSE AND UNKNOWN` = `FALSE`
    - `UNKNOWN AND UNKNOWN` = `UNKNOWN`
- **`OR`**
    - `UNKNOWN OR TRUE` = `TRUE`
    - `UNKNOWN OR FALSE` = `UNKNOWN`
    - `UNKNOWN OR UNKNOWN` = `UNKNOWN`
- **`NOT`**
    - `NOT UNKNOWN` = `UNKNOWN`

The result of `WHERE` clause predicate is treated as `FALSE` if the value evaluates to `UNKNOWN`.

## `IS NULL` and `IS NOT NULL`

The predicate `IS NULL` can be used to check for `NULL` values.

The predicate `IS NOT NULL` succeeds if the value on which it is applied is not `NULL`.