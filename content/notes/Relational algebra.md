---
title: "Relational algebra"
math: true
toc: true
---

A **relational algebra** is a procedural [[notes/Relational query language | query language]] consisting of a set of operations that take one or two relations as input and produce a new relation as their result.

There are six basic operators: $\sigma$(Selection), $\Pi$(Projection), $\cup$(Union), $-$(Set difference), $\times$(Cartesian product), and $\rho$(Rename).

Note that there are **equivalent queries**; there may be multiple ways to write a query in relational algebra.

## Selection

The unary selection operator $\sigma$ selects tuples that satisfy a given predicate.

- $\sigma_p(r)$, where $p$ is a selection predicate and $r$ is a relation.
    - e.g., $\sigma_{\texttt{building="E11"}}(\texttt{Department})$
- Comparisons uses $=, \neq, >, \geq, <, \leq$ in the selection predicate.
- Predicates are combined using $\wedge, \vee, \neg$.
- The select predicate may include comparisons between two different attributes.

## Projection

The unary projection operator $\Pi$ returns its argument relation with certain attributes removed.

- $\Pi_{A_1, \cdots, A_k}(r)$, where $A_i$s are attributes and $r$ is a relation.
    - e.g., $\Pi_{\texttt{ID,name,salary}}(\texttt{Instructor})$
- Duplicate rows are removed from the result

## Cartesian Product

The binary cartesian operator $\times$ combines information from two relations.

 It constructs a tuple of the result out of *each possible pair of tuples*.

- $r_1 \times r_2$, where $r_1$ and $r_2$ are relations.
    - e.g., $\texttt{Instructor} \times \texttt{Teaches}$
- To distinguish between attributes present in both relations, attach the name of the originating relation to the name of the attribute.
    - e.g., $\texttt{Instructor}.\texttt{ID}, \texttt{Teaches}.\texttt{ID}$

### Join

Join operator $\bowtie$ is a composition of a cartesian product followed by a selection operation.

It returns only those tuples that satisfy some predicate(s), among all possible combinations of tuples from the two relations.

It does *not* belong to the six basic operations.

- $r_1\bowtie_\theta r_2 := \sigma_\theta(r_1\times r_2)$, where $r_1(R_1)$, $r_2(R_2)$ are relations, and $\theta$ is a predicate on attributes on the schema $R_1 \cup R_2$.
    - e.g., $\texttt{Instructor} \bowtie_{\texttt{Instructor.ID=Teaches.ID}}\texttt{Teaches}$

## Union

The binary union operator $\cup$ combines two relations.

It returns all tuples that are present in at least one of the relations.

Two relations *must* satisfy the [[notes/Relational algebra#Condition | condition]].

- $r_1 \cup r_2$, where $r_1$ and $r_2$ are relations.
    - e.g., Find all courses taught in fall 2017, or in spring 2018, or in both:
    $$
        \Pi_{\texttt{courseID}}(\sigma_{\texttt{semester="Fall"}\wedge\texttt{year=2017}}(\texttt{Section})) \cup \\
        \Pi_{\texttt{courseID}}(\sigma_{\texttt{semester="Spring"}\wedge\texttt{year=2018}}(\texttt{Section})
    $$

### Intersection

The binary union operator $\cap$ combines two relations.

It returns all tuples that are present in both of the relations.

Two relations *must* satisfy the [[notes/Relational algebra#Condition | condition]].

- $r_1 \cap r_2$, where $r_1$ and $r_2$ are relations.

## Set Difference

The binary union operator $-$ combines two relations.

It returns all tuples that are present in the preceding relation, but not in the succeeding relation.

Two relations *must* satisfy the [[notes/Relational algebra#Condition | condition]].

- $r_1 - r_2$, where $r_1$ and $r_2$ are relations.

## Rename

The unary rename operator $\rho$ assigns a name to the results of relational algebra expressions.

It returns the result of the expression under the given name.

- $\rho_{x(A_1, \cdots, A_k)}(E)$, where $A_i$s are attributes, $E$ is a relational algebra expression, and $x$ is a name.

### Assignment

Assignment operation $\leftarrow$ assigns a relational algebra expression to a temporary relation variable.

It acts similar as the assignment operation in general-purpose programming languages.

- $x \leftarrow E$, where $x$ is a name and $E$ is a relational algebra expression.
    - e.g., Find all instructors in any of the Physics or Music departments:
  
    $\texttt{PH} \leftarrow \sigma_{\texttt{deptname="Physics"}}(\texttt{Instructor})$

    $\texttt{MU} \leftarrow \sigma_{\texttt{deptname="Musics"}}(\texttt{Instructor})$
    
    $\texttt{PH} \cup \texttt{MU}$
- With the assignment operation, a query can be written as a sequential program consisting of a series of assignments, followed by an expression whose value is displayed as the result of the query.

---

#### Condition
> - Two relations must have the same arity.
> - The attributes of the two relations must be compatible.