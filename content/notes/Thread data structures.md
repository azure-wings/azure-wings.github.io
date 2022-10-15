---
title: "Thread data structures"
math: true
toc: true
---

![thread-data-structure](/notes/images/thread-data-structure.png)

## Per-Thread State and Thread Control Block (TCB)
The operating system needs a data structure to represent a threads's state. This data structure is called the **thread control block (TCB)**. For every thread the operating system creates, it creates one TCB.

The thread control block holds two types of per-thread information:
- **Per-thread Computation State**
- **Per-thread Metadata**

### Per-thread Computation State
To create multiple threads and to be able to start/stop each thread as needed, the operating system must allocate space in the TCB for the _current state of each thread's computation_. This, in turn, is the **pointer to the thread's stack** and a **copy of its processor registers**.

- **Stack**
	- A thread's stack is the same as the stack for a single-threaded computation. It stores information needed by the nested procedures the thread is currently running.
	- Each thread needs its own stack, because at any given time different threads can be in different states in their sequential computations.
	- When a new thread is created, the operating system allocates it a new stack and stores a pointer to that stack in the thread's TCB.

- **Copy of processor registers**
	- A processor's registers include not only its general-purpose registers (for storing intermediate values for ongoing computations), but they also include special-purpose registers, such as the _instruction pointer_ and the _stack pointer_.
	- To be able to suspend/run/resume threads, the operating system needs a place to store a thread's registers when that thread is not actively running.

### Per-thread Metadata
The TCB also includes **per-thread metadata**, information for managing the thread. This includes _thread ID (tid)_, _scheduling priority_, and _status_.

## Shared State
Some state is **shared** between threads running _in the same process_ or _within the operating system kernel_. The followings are examples of shared states between threads.

- Program **code** is shared by all threads in a process (although each thread may be executing at a different place within that code).
- Statically allocated **global variables** and dynamically allocated **heap variables** can store information accessible to all threads.