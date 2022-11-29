---
title: "Primary key(E-R)"
math: true
toc: true
---

[[notes/Keys|Primary keys]] provide a way to specify how entities and relationships are distinguished.

## Primary key for [[notes/Entity set|entity sets]]

By definition, individual entities are distinct. However, from a database perspective, the differences among them must be expressed in terms of their attributes.

Therefore, the values of the attribute values of an entity must be such that theycan _uniquely identify_ the entity.

The concepts of superkey, candidate key, and primary key are applicable to entity sets just as they are applicable to [[notes/Structure of relational databases|relation schemas]].

## Primary key for [[notes/Relationship set|relationship sets]]

To distinguish among the various relationships of a relationship set, the **individual primary keys of the entities** in the relationship set are used.

Let $R$ be a relationship set involving entity sets $E_1, \cdots, E_n$. Let $A = \{ a_1, \cdots, a_m \}$ be the set of attributes assoiciated with $R$, which may be $\emptyset$. Then, the set of attributes

$$
\left( \bigcup_{i=1}^n \texttt{primary-key}(E_i) \right) \cup A
$$

forms a primary key for $R$.

The choice of the primary key for a relationship set depends on the [[notes/Constraint(E-R)#Mapping cardinality|mapping cardinality]] of the relationship set.