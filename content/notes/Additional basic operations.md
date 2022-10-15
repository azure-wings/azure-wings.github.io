---
title: "Additional basic operations"
math: true
toc: true
---

## Rename Operation

SQL allows renaming relations and attributes using the `AS` clause.

```sql
old_name AS new_name
```

The keyword `AS` is optional and may be omitted.

## String Operation

SQL includes a string matching operator for comparisons on character strings.\

```sql
LIKE some_string
```

The operator `LIKE` uses patterns; they can be described using two special characters: `%` and `_`.

- `%`: Matches any string.
- `_`: Matches any character.

Patterns are case-sensitive. SQL supports a variety of string operations such as:

- `str1 || str2`: Concatenate `str1` and `str2`.
- `UPPER(str)`, `LOWER(str)`: Converting from lower to upper / upper to lower cases.
- `LENGTH(str)`: Finding the length of `str`.
- `SUBSTR(str, start, length)`: Extracting substring.

### Escape Character

For patterns to include the special pattern characters (% and _), SQL allows the specification of an **escape character** defined using the `ESCAPE` keyword.

```sql
LIKE some_string ESCAPE escape_character
```

For example,

- `LIKE 'ab\%cd%' ESCAPE '\'` matches all strings beginning with `'ab%cd'`.
- `LIKE 'ab\\cd%' ESCAPE '\'` matches all strings beginning with `'ab\cd'`.

## Ordering the Display of Tuples

The `ORDER BY` clause causes the tuples in the results of a query to appear in sorted order.

```sql
ORDER BY some_attribute
```

We may specify `DESC` for descending order or `ASC` for ascending order; ascending order is the default setting.

`ORDER BY` can sort on multiple attributes.

## `WHERE` Clause Predicates

SQL includes a `BETWEEN` comparison operator to simplify `WHERE` clauses.

```sql
WHERE some_attribute BETWEEN start_val AND end_val
```

SQL allows the use of the notation `(v_1, ... , v_n)` to denote a tuple of arity `n` containing values `v_1`, … , `v_n`.

The comparison operator can be used on tuples, and the ordering is defined lexicographically.

- e.g., `(a_1, a_2) <= (b_1, b_2)` is true if both `a_1 <= b_1` and `a_2 <= b_2`.