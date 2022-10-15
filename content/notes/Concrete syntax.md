---
title: "Concrete syntax"
math: true
toc: true
---

**Concrete syntax** determines whether a certain string is a program or not.

## Intuition
Let $C$ be the set of all characters. Then, the set of all strings $S$ can be defined as
$$
S = \lbrace c_1c_2\cdots c_n : c_i \in C \rbrace.
$$
Concrete syntax defines which strings are considered as programs. Let $P$ be the set of all possible programs. In other words,
$$
P = \lbrace p: p \;\text{is a program} \rbrace.
$$
It is clear that $P \subseteq S$. Concrete syntax determines which elements $s \in S$ are in $P$. 

However, $P$ is (in most cases) an infinite set. Hence a sophisticated way to define concrete syntax is required.

## Backus-Naur Form (BNF)
BNF is one of the most popular method to define a concrete syntax. It consists of three concepts: **terminals**, **non-terminals**, and **expressions**.

### Terminals
A terminal is a string. `"00"`, `"abc"` are examples of terminals. Simple!

### Non-terminals
A non-terminal, also called a **metavariable**, denotes a set of strings. In BNF, it is denoted as a name between a pair of angle brackets. `<digit>`,`<expression>` are examples of non-terminals.

### Expressions
An expression is an enumeration of one or more terminals/nonterminals. The followings are all examples of expressions.
- `"abc"`
- `"0"` `"1"`
- `<digit>`
- `<digit>` `<number>`
- `"-"` `<number>`

Now, it is possible to construct a concrete syntax in BNF. In BNF, a definition of a set is denoted as:

`[nonterminal] ::= [expression] | [expression] | ...`

where the vertical bars separates distinct expressions.

An example of BNF can be given as:
```
<digit>  ::= "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9"
<nat>    ::= <digit> | <digit> <nat>
<number> ::= <nat> | "-" <nat>
```