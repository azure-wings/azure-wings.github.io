---
title: "Keys"
math: true
toc: true
---

We must have a way to specify how tuples within a given relation are distinguished; no two tuples in a relation are allowed to have exactly the same value for all attributes.

Let $K \subseteq R$, where $R$ is a [relation schema](Structure%20of%20Relational%20Databases%209c04c2584af142379f668c5078a9d46d.md) for the relation $r$.

- **Superkey**: $K$ is a **superkey** of $R$ if value for $K$ are sufficient to identify a unique tuple of each possible relation instance $r(R)$.
    - i.e., $\forall \;t_1, t_2 \in R: t_1 \neq t_2 \Rightarrow t_1.K \neq t_2.K$
- **Candidate key**: A superkey $K$ is a **candidate** key if $|K|$ is at its minimum value.
- **Primary key**: One of the candidate keys is selected to be the **primary key**.
    - Usually the most efficient one in terms of computation cost is chosen.
    - Primary key is chosen by the database designer as the principal means of identifying tuples within a relation.
    - Also referred to as the **primary key constraint**.

Let $A_i$ be an attribute of relations $r_i$.

- A **foreign-key constraint** from attribute(s) $*A_1$* of relation $*r_1*$ to the primary-key $A_2$ **of relation $*r_2*$ states that on any database instance, the value of $A_1$ **for each tuple in $*r_1*$ must also be the value of $A_2$ **for some tuple in $*r_2*$.
    - i.e., $\forall \, t_1 \in R_1: \exists \,t_2 \in R_2$ such that $t_1.A_1 = t_2.A_2$
- Attribute set $A_1$ **is called a **foreign key** from $*r_1*$, referencing $*r_2*$.
    - The relation $*r_1*$ is also called the **referencing relation**; $r_2$ is also called the **referenced relation**.