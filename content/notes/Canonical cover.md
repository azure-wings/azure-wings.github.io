---
title: "Canonical cover"
math: true
toc: true
---

## Extraneous attribute

Some attributes in a given relational schema do not affect the [[notes/Closure(Database)|closure of functional dependency]] of the schema.

An attribute of [[notes/Functional dependency|functional dependency]] in $F$ is said to be **extraneous** if it can be removed without changing its closure $F^+$.

When removing an attribute from a functional dependency:

- Removing an attribute from the **left** side of a functional dependency could make it a **stronger** constraint.
- Removing an attribute from the **right** side of a functional dependency could make it a **weaker** constraint.

Consider a set $F$ of functional dependencies and a functional dependency $\alpha \to \beta \in F$. Then attribute $A$ is **extraneous** if:

- $A \in \alpha$:\
  $F$ logically implies $\left( F \setminus \lbrace \alpha \to \beta \rbrace \right) \cup \lbrace (\alpha \setminus A) \to \beta \rbrace$
- $A \in \beta$:\
  $\left( F \setminus \lbrace \alpha \to \beta \rbrace \right) \cup \lbrace \alpha \to (\beta \setminus A) \rbrace$ logically implies $F$.

Note that a stronger functional dependency **always** implies a weaker one.

### Testing if an attribute is extraneous

Let $R$ be a relation schema, and let $F$ be a set of functional dependencies that hold on $R$.

Consider an attribute $A$ in the functional dependency $\alpha \to \beta \in F$.

- Testing if $A \in \alpha$ is extraneous in $\alpha$:
  1. Let $\gamma = \alpha \setminus A$.
  2. Compute $\gamma^+$ under $F$.
  3. If $\beta \subseteq \gamma^+$, $A$ is extraneous in $\alpha$.
- Testing if $A \in \beta$ is extraneous in $beta$:
  1. Let $F' = (F \setminus \lbrace \alpha \to \beta \rbrace) \cup \lbrace \alpha \to (\beta \setminus A) \rbrace$
  2. Compute $\alpha^+$ under $F'$.
  3. If $A \in \alpha^+$, $A$ is extraneous in $\beta$.

## Canonical cover

A **canonical cover** for $F$ is a set of dependencies $F_c$ that satisfies all of the followings:
- $F$ logically implies **all** dependencies in $F_c$.
- $F_c$ logically implies **all** dependencies in $F$.
- None of the attributes in $F_c$ is extraneous.
- Each left side of all functional dependencies in $F_c$ is unique.
  - i.e., $\forall \alpha_1 \to \beta_1, \alpha_2 \to \beta_2 \in F_c: \alpha_1 \neq \alpha_2$

### Purpose of canonical covers