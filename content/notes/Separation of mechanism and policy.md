---
title: "Separation of mechanism and policy"
math: true
toc: true
---

## Definition
The separation of **mechanism** and **policy** is a design principle in computer science. According to the separation of mechanism and policy principle, mechanism should work no matter what policy is used.

- **Mechanism** is a part of a system implementation that control the authorisation of operations and the allocation of resources.
- **Policy** determines _which_ decisions are made about which operations to authorise, and which resources to allocate.

For example, when considering a [thread context switch](notes/Mode%20transfer.md), **mechanism** decides _how to switch between threads_, and **policy** determines _which thread to run next_.