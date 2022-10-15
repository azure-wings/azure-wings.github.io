---
title: "Dual-mode operation"
math: true
toc: true
---


## Definition
**Dual-mode operation** of a kernel consists of two modes: **user mode** and **kernel mode**. 

- In **user mode**, the processor checks each instruction before executing it to verify that it is permitted to be performed by that process.
- In **kernel mode**, the operating system executes it with protection checks turned off.

## Hardware Requirements
The following three things must be supported by the hardware in order to accomplish dual-mode operation.

1. **Privileged Instructions**: All potentially unsafe instructions are prohibited when executing in user mode.
2. **Memory Protection**: All memory accesses outside of a process's valid memory region are prohibited when executing in user mode.
3. **Timer Interrupts**: The kermnel must have a way to periodically regain control from the current process, regardless of what the process does.

### Privileged Instructions
Instructions that are available in kernel mode, but not in user mode, are called **privileged instructions**. The followings are examples of privileged instructions.

- Changing the set of memory locations an application can access
- Disabling processor interrupts
- Changing an application's prvilige level
- Jumping into kernel code

If an application attempts to execute an instruction that is prvileged, **processor exception** is caused. This causes the processor to transfer control to an **exception handler** in the operating system kernel.

However, in some cases, applications must execute a privileged instruction. In such cases, applications are allowed to use a special instruction called **system call**. Processes can indirectly change their privilege level by executing a system call to transfer control into the kernel at a fixed location defined by the operating system.

### Memory Protection
To make memory sharing safe, an application must be prevented from reading/writing other applications' memory. Most modern processors introduce **virtual memory** to accomplish this.

With virtual memory, every process's memory starts at the same location (e.g., zero). The hardware translates these virtual addresses into physical memory locations. At runtime, **memory-management unit (MMU)** relocates each `load`/`store` instructions; if the given virtual address is illegal, MMU raises a **segmentation fault**.

### Timer Interrupts
If the user program enters an infinite loop (process monopolising CPU), or if the user simply becomes impatient and wants the system to stop the application, then the operating system must be able to regain control from applications. Operating system also needs to regain control of the processor in normal operations for multi-tasking.

A physical timer included in the computer system delivers a hardware signal (interrupt) to the processor with a predefined frequency set by the kernel. (Each timer interrupts only one processor.) When the timer interrupt occurs, the hardware transfers from the user process to the kernel (interrupt handler) running in kernel mode.

 However, interrupts can be temporarily deferred by the kernel. This is crucial for the implementation of [mutual exclusion].