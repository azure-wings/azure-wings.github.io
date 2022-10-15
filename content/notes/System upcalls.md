---
title: "System upcalls"
math: true
toc: true
---

## Necessity of System Upcalls
To allow applications to implement operating system-like functionality, more than [system call](notes/Mode%20transfer.md#System%20Calls) is required; applications can also benefit from being told when events occur that _need their immediate attention_. Such _virtualised_ interrupts and exceptions are called **upcalls**, also known as **signals** (in UNIX).

## Uses of System Upcalls
### Preemptive user-level threads
An application may run multiple tasks, or threads, in a process.

### Asynchronous I/O notification (`async` / `await`)
In an asynchronous I/O, a system calls starts the request and returns immediately. Later, the application can poll the kernel for I/O completion, or a separate notification can be sent via an upcall to the application when the I/O completes.

### Interprocess communication
A kernel upcall is needed if a process generates an event that needs the instant attention of another process.

### User-level exception handling
Applications may have their own exception handling routines. For this, the operating system needs to inform the application when it receives a processor exception.

### User-level resource allocation
Many applications are able to optimise their behaviour to differing amounts of CPU time or memory.
- e.g., Java garbage collection

## Diagrams
- The state of the user program and signal handler before a UNIX signal
![upcall-before](/notes/images/upcall-before.png)

- The state of the user program and signal handler during a UNIX signal
![upcall-during](/notes/images/upcall-during.png)

## Comparison with [interrupts](notes/Mode%20transfer.md#Interrupts)
### Types of Signals
- In place of hardware-defined interrupts and processor exceptions, the kernel defines a limited number of sifnal types that a process can receive.

### Handlers
- The kernel defines its own [interrupt vector](notes/Implementation%20of%20mode%20transfer.md#Interrupt%20Vector).
- Each process defines its own signal handlers for each signal type.

### Signal Stack
- The kernel uses [interrupt stack](notes/Implementation%20of%20mode%20transfer.md#Interrupt%20Stack), a region of _kernel_ memory when handling interrupts.
- Applications have the option to run UNIX signal handlers on the process's _normal execution stack_, or on a special **signal stack** allocated buy the user process in user memory.

### Signal Masking
- The kernel can defer the arrival of interrupts via [interrupt masking](notes/Implementation%20of%20mode%20transfer.md#Interrupt%20Masking).
- UNIX defers signals for events that occur while the signal handler for those types of events is in progress.
- The deferred signal is delivered once the handler returns to the kernel.

### Processor State
- The _kernel_ copies onto the signal stack the saved state of the program counter, stack pointer, and general-purpose registers at the point when the program stopped.
- When the signal handler returns, the kernel reloads the saved state into the processor to resume program execution.
- The signal handler can also _modify_ the saved state, so that the kernel resumes a different user-level task on return.