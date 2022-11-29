---
title: "Extended E-R features"
math: true
toc: true
---

## Specialisation

An [[notes/Entity set|entity set]] may include subgrouping of entities that are distinct in some way from other entities in the set. The process of designating subgroups within an entity set is called **specialisation**.

These subgroupings become _lower-level entity sets_ that have attributes or participate in relationships that do not apply to the higher-level entity set.

## Generalisation

**Generalisation** is a containment relationship that exists between a higher-level entity set and one or more lower-level entity sets. This is a **bottom-up** design process, in which multiple entity sets are synthesised into a higher-level entity set on the basis of _common features_.

The terms specialisation and generalisation are used interchangeably.

## Attribute inheritance

A lower-level entity set inherits all the attributes and relationship participation of the higher-level entity set to which it is linked. This is called **attribute inheritance**.

Lower- and higher-level entity sets are also referred to as **subclasses** and **superclasses**, respectively.

## Constraints on specialisations/generalisations

To model an enterprise more accurately, the database designer may choose to place
certain constraints on a particular generalisation/specialisation.

### Disjoint/Overlapping specialisation

One type of constraint on specialisation specifies whether a specialisation is **disjoint** or **overlapping**.

- **Disjoint**\
    A _disjoint constraint_ requires that an entity belong to no more than one lower-level entity set.

- **Overlapping**\
    An _overlapping constraint_ requires that an entity may belong to more than one lower-level entity sets within a single specialisation.
    

### Completeness constraint

The **completeness constraint** specifies whether or not an entity in the higher-level entity set must belong to at least one of the lower-level entity sets within the generalisation.

- **Total**\
    Each higher-level entity _must_ belong to a lower-level entity set.

- **Partial**\
    Some higher-level entities may _not_ belong to any lower-level entity set.

Partial generalisation is the default.

## Aggregation

**Aggregation** is an abstraction through which relationships are treated as higher-level entities. By treating relationship as an abstract entity, relationships between relationships can be defined, thereby reducing unnecessary redundancy.