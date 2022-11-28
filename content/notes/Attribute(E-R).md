---
title: "Attribute(E-R)"
math: true
toc: true
---

An attribute of an [[notes/Entity set|entity set]] is a function that maps from the entity set into a domain. Since an entity set may have several attributes, each entity can be described by a set of (attribute, data value) pairs, one pair for each attribute of the entity set.

An attribute, as used in the E-R model, can be characterised by the following attribute types.

- **Simple** / **Composite**
  - **Simple** attributes are not divided into subparts (i.e., other attributes).
  - **Composite** attributes can be divided into subparts.
- **Single-valued** / **Multivalued**
  - **Single-valued** attributes have a single value for a particular entity.
  - **Multivalued** attributes have a set of values for a specific entity.
- **Derived**
  - The value of derived attributes can be derived from the values of other related attributes or entities.

An attribute takes a [[notes/Null values in SQL|null]] value when an entity does not have a value for it.