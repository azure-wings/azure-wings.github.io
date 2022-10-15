---
title: "Mode transfer"
math: true
toc: true
---

The operating system must provide a way to safely transfer between user mode and kernel mode. 

## User to Kernel Mode
There are three reasons for the kernel to take control from a user process: **interrupts**, **processor exceptions**, and **system calls**.

### Interrupts
An **interrupt** is an asynchronous signal to the processor that some external event has occurred that may require its attention. The followings are examples of interrupts.

- Processor timer
- I/O requests (keyboard, mouse, network, ...)

A processor checks for whether an interrupt has arrived as it executes and, if so, it completes or stalls any instructions that are in progress. On a multiprocessor, an interrupt is taken on only one of the processors. Each different type of interrupt requires its own **interrupt handler**.

### Processor Exceptions
A **processor exception** is a hadware event caused by (unexpected or malicious) user program behaviour that causes a transfer of control to the kernel. The followings are examples of processor exceptions.

- Performing privileged instruction
- Accessing memory outside accessible memory region (Segmentation fault)
- Dividing by zero
- Writing to read-only memory
- Accessing a word of memory with a non-aligned address
- Setting a breakpoint in a program

On a multiprocessor, the exception only stops execution on the processor triggering the exception. The kernel then needs to send interprocessor interrupts to stop execution of the parallel program on other processors.

### System Calls
User programs can voluntarily transition into the operating system kernel that the kernel perform an operation on the user's behalf. A **system call** is any procedure provided by the kernel that can be called from user level. The followings are examples of system calls.

- System call to send/receive packets over the network
- System call to create/delete files
- System call to read/write data into files
- System call to create new user process

To protect the kernel from misbehaving user programs, it is essential that the hardware transfers control on a ststem call to a _pre-defined_ address. Even with system calls, user processes cannot be allowed to jump to arbitrary places in the kernel.

## Kernel to User Mode
### New Process
To start a new process, the kernel copies the program into memorym, sets the program counter to the first instruction of the process, sets the stack pointer to the base of the user stack, and switches to user mode.

### Resume After an Interrupt, Processor Exception, or System Call
When the kernel finishes handling th erequest, it resumes the execution of the interrupted process by restoring its program counter, restoring its registers, and changing the mode back to user level.

### Switch to Different Process
The kernel save the process state of the old process in the process's control block. The kernel can then resume a different process by loading its state from the process's control block into the processor and then switching to user mode.

### User-level Upcall
Many operating systems provide user programs with the ability to receive any asynchronous notification or events.