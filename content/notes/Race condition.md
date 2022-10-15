---
title: "Race condition"
math: true
toc: true
---

## Definition
A **race condition** is a situation where multiple process access and manipulate _the same data_ concurrently, and the outcome of the execution depends on _the particular order_ (interleaving) of such accesses.

## Example
Suppose that initially `y = 12`, and a program with two threads that do the following is run.

| Thread A    | Thread B    |
| ----------- | ----------- |
| `x = y + 1` | `y = y * 2` |

- If thread A reads `y` before thread B updates `y`, the result is `x = 13`.
- Otherwise, the result is `x = 25`.

Suppose that initially `x = 0`, and a program with two threads that do the following is run.

| Thread A    | Thread B     |
| ----------- | ------------ |
| `x = 1`     | `y = 2`      |
| `x = y + 1` | `y = y * 2*` |

- If thread A runs to completion and then thread B starts and runs to completion, the result is `x = 1`.
- If thread B runs to completion and then thread A starts and runs to completion, the result is `x = 5`.
- If thread B executes `y = 2` and interleaves - thread A starts and runs to completion - and thread B executes `y = y * 2`, the result is `x = 3`.
- If thread A executes `x = 1` and interleaves - thread B starts and runs to completion - and thread A executes `x = y + 1`, the result is `x = 5`.