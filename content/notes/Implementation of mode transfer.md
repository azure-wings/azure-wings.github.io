---
title: "Implementation of mode transfer"
math: true
toc: true
---

## Importance
The context switch ([mode transfer](notes/Mode%20transfer.md)) must be carefully crafted, and it relies on _hardware support_. To avoid confusion and reduce the possibility of error, m most operating systems have a common sequence of instructions both for entering the kernel and for returning to user level, regardeless of te cause.

At a minimum, this common sequence must provide the followings.

- **Limited entry into the kernel**: User programs cannot be allowed to jump to arbitrary locations in the kernel.
- **Atomic changes to processor state**: Transitioning between kernel and user mode is [atomic](notes/Atomic%20operation.md); _the mode, program counter, stack and memory protection_ are all changed _<u>at the same time</u> (with a single instruction).
-  **Transparent, restatable execution**: The operating system must be able to restore the state of the user program exactly as it was before the context switch.

## Interrupt Vector
When an interrupt, processor exception or system call trap occurs, the operating system must take different actions depending on what the event is. To this end, the processor has a special register that points to an area of kernel memory called the **interrupt vector table** set up by the kernel.

The interrupt vector table is an array of pointers, with each entry pointing to the first instruction of a different handler procedure in the kernel. An **interrupt handler** is the term used for the procedure called by kernel on an interrupt.

![interrupt-vector-table](/notes/images/interrupt-vector-table.png)

## Interrupt Stack
**Interrupt stack** is a region of _kernel_ memory pointed by a special, privileged register. When an interrupt, processor exception, or system call trap causes a context switch into the kernel, the hardware changes the stack pointer to point to the base of the kernel's interrupt stack. The _hardware_ automatically saves some of the interrupted process's registers by pushing them onto the interrupt stack before calling the kernel's handler.

When the kernel handler handler runs, it pushes any remaining registers onto the stack before pereforming its work. When returning from the interrupt, processor exception or system call trap, the reverse occurs. The handler pops the saved registers and the hardware restores the registers it saved, returning back to the point where the processor was interrupted. When returning from a system call, the value of the saved program counter _must be incremented_.

On a multiprocessor, each processor needs to have its own interrupt stack so that the kernel can handle simultaneous system calls and exceptions aacross multiple processors.

### Two Stacks per Process
Most operating system kernels go one step further and allocate a kernel interrupt stack for every user-level process. This makes it easier to switch to a new process inside an interrupt or system call handler.

![interrupt-stack](/notes/images/interrupt-stack.png)

- If the process is running on the processor in user mode, its kernel stack is empty.
- If the process is running on the processor in kernel mode (regardless of cause), its kernel stack is in use, containing the saved registers from the suspended user-level computations and the current state of the kernel handler.
- If the process is available to run but is waiting on the processorm its kernel stack contains the registers and state to be restored when the process is resumed.
- If the process is waiting for an I/O event to complete, its kernel stack contains the suspended computation to be resumed when the I/O finishes.

## Interrupt Masking
In certain regions of the kernel such as interrupt handlers or a scheduler, taking an interrupt could cause confusion. In such cases, the hardware provides a _privileged instruction_ to temporarily defer the delivery of an interrupt until it is safe to do so.

If multiple interrupts arrive while interrupts are disabled, the hardware delivers them in turn when interrupts are re-enabled. However, due to the limited buffering of hardwares, some interrupts may be lost.

If the processor takes an interrupt in kernel mode with interrupts enabled, it is safe to use the current stack pointer rather than resetting it to the base of the interrupt stack.