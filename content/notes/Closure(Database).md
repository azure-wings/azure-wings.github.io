---
title: "Closure(Database)"
math: true
toc: true
---

## Closure of functional dependencies

Given a set $F$ of [[notes/Functional dependency|functional dependencies]], there are certain other functional dependencies that are logically implied by $F$.

The set of all functional dependencies logically implied by $F$ is called the **closure** of $F$, and is denoted as $F^+$.

### Armstrong's axioms

For any set $F$ of functional dependencies, the closure $F^+$ of $F$ can be obtained by repeatedly applying **Armstrong's axioms**.

Let $\alpha, \beta, \gamma, \delta$ be sets of attributes of a relation schema $R$ with the set of functional dependency $F$.

- **Reflexive rule**: $\beta \subseteq \alpha \Rightarrow \alpha \to \beta$
- **Augmentation rule**: $\alpha \to \beta \Rightarrow \forall \gamma: \gamma\alpha \to \gamma\beta$
- **Transitivity rule**: $\alpha \to \beta \land \beta \to \gamma \Rightarrow \alpha \to \gamma$

The above rules are both
- **Sound**: Generates only the functional dependencies that _actually hold_.
- **Complete**: Generates _all_ the functional dependencies that hold.

Some additional rules can be inferred from **Armstrong's axioms**.

- **Union rule**: $\alpha \to \beta \land \alpha \to \gamma \Rightarrow \alpha \to \beta\gamma$
- **Decomposition rule**: $\alpha \to \beta\gamma \Rightarrow \alpha \to \beta \land \alpha \to \gamma$
- **Pseudo-transitivity rule**: $\alpha \to \beta \land \gamma\beta \to \delta \Rightarrow \alpha\gamma \to \delta$

## Closure of attribute sets

Similarly as [[notes/Functional dependency|functional dependencies]], a **closure** of an attribute set $\alpha$ under $F$, denoted by $\alpha^+$, can be defined.

The set of all attributes that are functionally determined by $\alpha$ under $F$ are called the **closure** of $\alpha$, and is denoted as $\alpha^+$.

### Usages of attribute closures

Attribute closures can be used for various purposes:

- **Testing for [[notes/Keys|superkey]]**
  - Testing if $\alpha$ is a superkey can be done by checking if $R \subseteq \alpha^+$.
- **Testing functional dependencies**
  - Testing if a functional dependency $\alpha \to \beta$ is in $F^+$ can be done by checking $\beta \subseteq \alpha^+$.
- **Computing the closure $F^+$**
  - $F^+$ can be obtained by finding $\gamma^+$ for each $\gamma \subseteq R$, and for each $S \subseteq \gamma^+$, outputting a functional dependency $\gamma \to S$.

## Algorithms for computing closures

### Algorithm for computing $F^+$

```
F_closure = F
REPEAT
  FOR EACH f IN F_closure
    APPLY reflexivity AND augmentation ON f
    ADD TO F_closure
  FOR EACH PAIR f1, f2 IN F_closure
    IF f1 AND f2 APPLY transitivity
    THEN ADD TO F_closure
UNTIL (F_closure CONVERGE)
```

### Algorithm for computing $\alpha^+$

```
A_closure = A
REPEAT
  FOR EACH beta -> gamma IN A
    IF beta IN A_closure
    THEN ADD gamma TO A_closure
UNTIL (A_closure CONVERGE)
```