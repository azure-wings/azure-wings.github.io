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

Let $R$ be a relationship set involving entity sets $E_1, \cdots, E_n$. Let $A = \lbrace a_1, \cdots, a_m \rbrace$ be the set of attributes assoiciated with $R$, which may be $\emptyset$. Then, the set of attributes

$$
\left( \bigcup_{i=1}^n \texttt{primary-key}(E_i) \right) \cup A
$$

forms a primary key for $R$.

The choice of the primary key for a relationship set depends on the [[notes/Constraint(E-R)#Mapping cardinality|mapping cardinality]] of the relationship set.

## Weak entity sets

In some cases, the primary key of an entity in a relationship is redundant when describing the relationship. In this case, an alternative way to deal with this redundancy is to not store the redundant attribute in the entity.

A **weak entity** is one whose existence is dependent on another entity, called its **identifying entity**. An entity set that is not a weak entity set is termed a **strong entity set**.

Instead of associating a primary key with a weak entity, we use the identifying entity, along with extra attributes called a **discriminator** or **partial key** to uniquely identify a weak entity.

Every weak entity _must_ be associated with an identifying entity; the weak entity set is said to be **existence dependent** on the identifying entity set.
- The identifying entity set is said to **own** the weak entity set that it identifies.
- The relationship associating the weak entity set with the identifying entity set is called the **identifying relationship**.