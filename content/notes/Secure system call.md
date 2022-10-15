---
title: "Secure system call"
math: true
toc: true
---

## Importance
The kernel must implement its system calls in a way that protects itself from all errors and attacks that might be launched by the misuse of the interface. That is, the kernel should always assume that the parameters passed to a system call are intentionally designed to be as _malicious_ as possible.

## Implementation of a Secure System Call

![secure-syscall](/notes/images/secure-syscall.png)

1. The user program calls the user stub in the normal way, oblivious to the fact the implementation of the procedure is in fact in the kernel.
2. The user stub fills in the code for the system call and executes the trap instruction.
3. The hardware transfers control to the kernel, vectoring to the system call handler. The handler acts as a stub on the kernel side, **copying** and checking arguments and then calling the kernel implementation of system call.
4. After the system call completes, it returns to the handler.
5. The handler returns to user level at the next instruction in the stub.
6. The stub returns to the caller.

## Tasks of the Kernel Stub
### Locate system call arguments
Unlike a regular kernel procedure, the arguments to a system call are stored in user memory. Since the user stack pointer may be corrupted, the stub must check the address to verify whether the pointer argument is a legal address within the user domain. If it is legal, the stub converts the virtual address into a physical address.

### Validate parameters
The kernel must protect itself against malicious or accidental errors in the format or content of its arguments. If an error is detected, the kernel returns to the user program.

### Copy before check
An application might modify the parameter _after_ the stub checks its value but _before_ the parameter is used in the actual implementation of the routine. This is called a **time of check vs. time of use (TOCTOU) attack**. To prevent this, kernel copies the system call parameters into kernel memory before performing the necessary checks.

### Copy back any results
For the user program to access the results of the system call, the stub must copy the result from the kernel into user memory. The kernel must translate the physical address into virtual address before performing the copy.