---
title: "x86 Mode Transfer"
math: true
toc: true
---

## Background on x86 Architecture
x86 is segmented, so pointers come in two parts.

- **Segment**: A region of memory such as code, data, or stack
- **Offset**: An offset within that segment

The current user-level instruction is a combination of the code segment (`cs`) and the instruction pointer (`eip` / `rip`) within the code segment. The current stack position is a combination of the stack segment (`ss`) and the stack pointer (`esp` / `rsp`) within the stack segment.

The current privilege level is stored as the low-order buts of the `cs` register. The `eflags` register has condition codes that are modified as a by-product of executing instructions, as well as other flags that control the processor's behaviour (such as whether interrupts are masked).

## Mode Transfer in x86
When a processor exception or a system call trap occurs, the following procedure takes place.

1. **Mask interrupts**.
	- The hardware prevents any interrupts from occurring while the processor is in the middle of context switch.
2. **Save three key values**. 
	- The hardware saves the values of the stack pointer (`esp`/`rsp` and `ss`), the execution flags (`eflags`), and the instruction pointers (`eip`/`rip` and `cs`) to internal, temporary hardware registers.
3. **Switch onto the kernel interrupt stack**.
	- The hardware switches the stack segment / stack pointer to the base of the kernel interrupt stack as specified in a special hardware register.
4. **Push the three key values onto the new stack**.
	- The hardware stores the internally saved values onto the stack.
5. **Optionally save an error code.**
	- The hardware pushes an error code (generated by certain types of exceptions, e.g., page fault) and make it the top item on the stack. For other types of events, the software interrupt handler pushes a dummy value onto the stack.
6. **Invoke the interrupt handler**.
	- The hardware changes the code segment / program counter to the address of the interrupt handler procedure.
	- The handler pushes the rest of the registers, including the current stack pointer (but not the instruction pointer or `eflags` register), onto the stack.

- State of the system before an interrupt handler is invoked
![x86-mode-switch-1](/notes/images/x86-mode-switch-1.png)

- State of the system after the jump to the interrupt handler
![x86-mode-switch-2](/notes/images/x86-mode-switch-2.png)

- State of the system after the interrupt handler has started executing
![x86-mode-switch-3](/notes/images/x86-mode-switch-3.png)

When the handler completes, it can resume the interrupted process. The handler executes the x86 `iret` instruction. It [atomically](notes/Atomic%20operation.md) restores the program counter, program stack pointer, the processor status word/condition codes, and switches the process back to user mode.