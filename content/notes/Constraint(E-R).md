---
title: "Constraint(E-R)"
math: true
toc: true
---

An E-R enterprise schema may define certain constraints to which the contents of a database must conform.

## Mapping cardinality
**Mapping cardinality** expresses the number of entities to which another entity can be associated via a relationship set. It is most useful in describing binary relationship sets.

For a binary relationship set $R$ between entity sets $A$ and $B$, the mapping cardinality must be one of the following:
- **One-to-one**
- **One-to-many**
- **Many-to-one**
- **Many-to-many**

### One-to-one
An entity in $A$ is associated with _at most_ one entity in $B$, and vice versa.

![one-to-one-mapping-example](notes/images/one-to-one-mapping-example.png)

### One-to-many
An entity in $A$ is associated with any number (zero or more) of entities in $B$. An entity in $B$ can be associated with _at most_ one entity in $A$.

![one-to-many-mapping-example](notes/images/one-to-many-mapping-example.png)

### Many-to-one
An entity in $A$ can be associated with _at most_ one entity in $B$. An entity in $B$ is associated with any number (zero or more) of entities in $A$.

![many-to-one-mapping-example](notes/images/many-to-one-mapping-example.png)

### Many-to-many
An entity in $A$ is associated with any number (zero or more) of entities in $B$, and vice versa.

![many-to-many-mapping-example](notes/images/many-to-many-mapping-example.png)

## Participation constraints

Let $E$ be an entity set and $R$ be a relationship set.

- **Total participation**

    The participation of $E$ in $R$ is said to be **total** if every entity in $E$ participates in at least one relationship of $R$.

- **Partial participation**
  
    The participation of $E$ in $R$ is said to be **partial** if only some entities in $E$ participate in relationships in $R$.