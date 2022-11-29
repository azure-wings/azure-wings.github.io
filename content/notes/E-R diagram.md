---
title: "E-R diagram"
math: true
toc: true
---

## Basic structure

An E-R diagram consists of the following major components:

- **Rectangles divided into two parts**

    Represent entity sets. The first part contains the name of the entity set. The second part contains the names of all the attributes of the entity set.

- **Diamonds**

    Represent relationship sets.

- **Undivided rectangles**

    Represent the attributes of a relationship set. Attributes that are part of the primary key are underlined.

- **Lines**
  
    Link entity sets to relationship sets.

- **Dashed lines**

    Link attributes of a relationship set to the relationship set.

- **Double lines**

    Indicate [[notes/Constraint(E-R)#Participation constraints|total participation]] of an entity in a relationship set.

- **Double diamonds**

    Represent identifying relationship sets linked to weak entity sets.

![er-diagram-basics](notes/images/er-diagram-basics.png)

## [[notes/Constraint(E-R)#Mapping cardinality|Mapping Cardinality]]

To distinguish among different mapping cardinalities, either a directed line $(\rightarrow)$, signifying '**one**', or an undirected line $(-)$, signifying '**many**', is drawn between the relationship set and the entity set.

![er-diagram-mapping-cardinality](notes/images/er-diagram-mapping-cardinality.png)

E-R diagrams also provide a way to indicate more complex constraints on the number of times each entity participates in relationships in a relationship set.

A line may have an associated minimum and maximum cardinality, shown in the form $l..h$, where $l$ is the minimum and $h$ is the maximum capacity. The $*$ sign indicates 'no limit'.

![er-diagram-complex-cardinality](notes/images/er-diagram-complex-cardinality.png)

## [[notes/Attribute(E-R)|Complex attributes]]

E-R diagrams can also describe complex attributes.

**Composite attributes** and **component attributes** are distinguished with indentations. Component attributes that consists the composite attributes are given directly below the composite attribute with an indentation.

**Multivalued attributes** are written inside curly braces $( \{ \cdots \} )$.

**Derived attributes** are written with an additional parentheses at the end.

![er-diagram-complex-attributes](notes/images/er-diagram-complex-attributes.png)

## [[notes/Relationship set|Roles]]

Roles are indicated in E-R diagrams by labeling the lines that connect diamonds to rectangles.

![er-diagram-roles](notes/images/er-diagram-roles.png)

## [[notes/Relationship set#Nonbinary relationship sets|Nonbinary relationship sets]]

_At most_ one arrow out of a ternery (or greater degree) relationship is allowed to indicate a cardinality constraint.

If there are more than arrow, there are two ways of interpreting the meaning. Suppose that there is a relationship set $R$ between entity sets $A_1, \cdots, A_n$, and the only arrows are on the edges to entity sets $A_{i+1}, A_{i+2}, \cdots, A_n$.
- A particular _combination_ of entities from $A_1, \cdots, A_i$ can be associated with at most one _combination_ of entities from $A_{i+1}, \cdots, A_n$.
  - i.e., the primary key for the relationship $R$ can be constructed by the union of the primary keys of $A_1, \cdots, A_i$.
- For each entity set $A_k (i < k \leq n)$, each combination of the entities from the other entity sets can be associated with at most one entity from $A_k$.
  - i.e., Each set $\{ A_1, \cdots, A_{k-1}, A_{k+1}, \cdots, A_n \}$, for $i < k \leq n$, forms a candidate key.

[[notes/Functional dependencies]] allow either of these interpretations to be specified in an unambiguous manner.

## Weak entity sets
