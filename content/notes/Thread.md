---
title: "Thread"
math: true
toc: true
---

A **thread** is a _single execution sequence_ that represents _a separately schedulable task_. Doing so, threads provide the illusion of an infinite number of _processors_.

- **Single execution sequence**: Each thread executes a sequence of instructions, just as in the familiar sequential programming model.
- **Separately schedulable task**: The operating system can run, suspend (block), or resume a thread at any time.

Threads can run either in a [process](notes/Process.md) or in the kernel; there is also _shared state_ that is not saved or restored when switching the processor between threads.

## Advantages
Using threads to express and manage concurrency has several advantages.

-  **Expressing logically concurrent tasks**: Threads eneable the expression of an application's natural concurrency by writing each concurrent task as a separate thread.
- **Shifting work to run in the background**: To improve user responsiveness and performance, a common design pattern is to create threads to perform work that in the background, without the user waiting for the result.
- **Exploiting multiple processors**: Programs can use threads on a multiprocessor to do work in parallel; they can do the same work in less time or more work in the same elapsed time.
- **Managing I/O devices**: By running tasks as separate threads, when one task is waiting for I/O, the processor can make progress on a different task.

## Comparison with [Processes](notes/Process.md)
- [Comparison between processes and threads](notes/Comparison%20between%20processes%20and%20threads.md)

## Thread Data Structures
- [Thread data structures](notes/Thread%20data%20structures.md)

## Thread Life Cycle
- [Thread life cycle](notes/Thread%20life%20cycle.md)
