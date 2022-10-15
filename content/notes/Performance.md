---
title: "Performance"
math: true
toc: true
---

## Defining Performance
- **Response time (execution time)**: The time between start and completion of a task
- **Throughput (Bandwidth)**: The number of tasks completed per unit time

## Measuring Performance
- **Clock cycle** (s): The time for one clock period (usually the processor clock) - constant
- **Clock rate** (Hz): The inverse of clock period
- **CPU execution time**: The time CPU spends computing for a certain task (does not include time spent waiting for I/O or running other programs)
$$
\begin{align*}
\text{CPU time} &= \text{CPU clock cycles} \times \text{Clock cycle time}\\
&= \frac{\text{CPU clock cycles}}{\text{Clock rate}}
\end{align*}
$$
- **CPI (Clock cycles per instruction)**: The average number of clock cycles per instruction for a program or program fragment.
$$
\begin{align*}
\text{CPU clock cycles} = \text{Total number of instructions} \times \text{CPI}
\end{align*}
$$
Therefore, we have the following.
$$
\begin{align*}
\text{CPU time} &= \frac{\text{Instruction count} \times \text{CPI}}{\text{Clock rate}}
\end{align*}
$$
