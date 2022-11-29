---
title: "Reduction to relational schema"
math: true
toc: true
---

[[notes/Entity set|Entity sets]] and [[notes/Relationship set|relationship sets]] can be expressed uniformly as [[notes/Structure of relational databases|relation schemas]] that represent the contents of the database.

A database which conforms to an [[notes/E-R diagram]] can be represented by a collection of schemas. For each entity set and relationship set, there is a _unique_ schema that is assigned the name of the corresponding entity set or relationship set. Furthermore, each schema has a number of columns (generally corresponding to attributes), which have unique names.

## Representing [[notes/Entity set|entity sets]]

- A **strong eneity set** reduces to a schema with the same attributes.
  - e.g., $\texttt{student(\underline{ID}, name, credits)}$
- A **[[notes/Primary key(E-R)#Weak entity sets|weak entity set]]** becomes a table that includes a column for the primary key of the identifying strong entity set.
  - e.g., $\texttt{section(\underline{courseID}, \underline{secID}, \underline{sem}, \underline{year})}$

### Entity sets with composite attributes

- **[[notes/Attribute(E-R)|Composite attributes]]** are flattened out by creating a separate attribute for each component attribute.
  - e.g., with composite attribute `name` with component attributes `firstName`, `middleName`, and `lastName`:\
    $\texttt{instructor(..., firstName, middleName, lastName, ...)}$

### Entity sets with multivalued attributes

- A **[[notes/Attribute(E-R)|multivalued attribute]]** $M$ of an entity $E$ is represented by a _separate schema_ $EM$.
- The schema $EM$ has attributes corresponding to the primary key of $E$, and an attribute corresponding to the multivalued attribute $M$.
  - e.g., Multivalued attribute `phoneNo` of `instructor` is represented by:\
    $\texttt{inst-phone(\underline{ID}, \underline{phoneNo})}$
- Each balue of the multivalued attribute maps to a separate tuple of the relation on the schema $EM$.

## Representing [[notes/Relationship set|relationship sets]]

### Relationship sets with different [[notes/Constraint(E-R)#Mapping cardinality|mapping cardinalities]]

- A **many-to-many** relationship is represented as a schema with attributes for the primary keys of the two participating entity sets, and any descriptive attributes of the relationship set.
  - e.g., Schema for a relationship set `advisor` between `student` and `instructor`:\
    $\texttt{advisor(\underline{studentID}, \underline{instructorID})}$
- **Many-to-one** and **one-to-many** relationship sets that are _[[notes/Constraint(E-R)#Participation constraints|total]]_ on the many-side can be represented by adding an extra attribute to the 'many' side, containing the primaty keys of the 'one' side.
  - e.g., Instead of creating a schema for a relationship set `inst-dept` between `instructor` and `department` with many-to-one mapping, add an attribute `deptName` to the schema arising from the entity set `instructor`.
  - If the [[notes/Constraint(E-R)#Participation constraints|participation]] if **partial** on the 'many' side, this could result in [[notes/Null values in SQL|null values]].
- A **one-to-one** relationship sets, either side can be chosen to act as the 'many' side.
  - An extra attribute can be added to either of the tables corresponding to the two entity sets.

## Redundancy of schemas

- The schema corresponding to a relationship set linking a [[notes/Primary key(E-R)#Weak entity sets|weak entity set]] to its identifying strong entity set is **redundant**.
  - e.g., The `section` schema already contains the attributes that would appear in the `sec-course` schema.

## Representing [[notes/Extended E-R features#Specialisation|specialisations]]

### Method 1
1. Form a schema for the higher level entity.
2. Form a schema for each of the lower level entity set, and include the primary key if the higher level entity set and local attributes.

e.g.,
| Schema | Attributes |
|--------|------------|
| person | ID, name, street, city |
| student | ID, credits |
| employee | ID, salary |

- **Drawbacks**: Accessing information about an lower level entity requires accessing two relations (the one corresponding to the lower level schema, and the one corresponding to the higher level schema).

### Method 2
1. Form a schema for each entity set with all local and inherited attributes.
  
e.g.,
| Schema | Attributes |
|--------|------------|
| person | ID, name, street, city |
| student | ID, name, street, city, credits |
| employee | ID, name, street, city, salary |

- **Drawbacks**: Some attributes may be stored redundantly for entities that belongs to two or more specialised entity sets.

## Representing aggregations

To represent [[notes/Extended E-R features#Aggregation|aggregations]], create a schema containing
- The primary key of the aggregated relationship
- The primary key of the associated entity set
- Any descriptive attributes

e.g.,

Consider the ternary relationship `proj-guide` between `instructor`, `student`, and `project`. Regard the relationship set `proj-guide` as a higher-level entity set. Create a binary relationship `eval-for` between `proj-guide` and `evaluation`.

The schema for `eval-for` is: $\texttt{eval-for(studentID, projectID, instructorID, evaluationID)}$