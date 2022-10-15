---
title: "Atomic operation"
math: true
toc: true
---

## Definition
An **atomic operation** is an _indivisible_ operation that _cannot be ineterleaved_ or split by other operations.

## Examples
- On most modern architectures, a `load` or `store` of a 32-bit word from or to memory is an atomic operation.
- However, depending on the hardware implementation, a `load` or `store` of a 64-bit word may not be atomic.