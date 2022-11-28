---
title: "Relationship set"
math: true
toc: true
---

A **relationship** is an association among several entities. A **relationship instance** in an E-R schema represents an association between the named entities in the real-world enterprise that is being modeled.

![relationship-example](/notes/images/relationship-example.png)

A **relationship set** is a set of relationships of the same type. Formally, it is a [[notes/Relation|mathematical relation]] on $n \geq 2$ [[notes/Entity set|entity sets]] that are not necessarily distinct.

If $E_1, \cdots, E_n$ are entity sets, then a relationship set $R$ is a subset of
$$
\{(e_1, \cdots, e_n) : e_i \in E_i, i = 1, \cdots, n\}
$$
where $(e_1, \cdots, e_n)$ is a relationship.

The entity sets $E_1, \cdots, E_n$ are said to **participate** in the relationship set $R$.

The function that an entity plays in a relationship is called that entity's **role**. Each occurrence of an entity set plays a role in the relationship. However, since entity sets participating in a relationship set are generally distinct, roles are implicit and are not usually specified.

An relationship may also have attributes called **descriptive attirbutes** that are associated with a relationship set.

![descriptive-attribute-example](/notes/images/descriptive-attribute-example.png)

The number of entity sets that participate in a relationship set is the **degree** of the relationship set.
- A binary set relationship set is of degree 2.
- A ternary set relationship set is of degree 3.