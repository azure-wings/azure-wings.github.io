---
title: "Thread life cycle"
math: true
toc: true
---

![thread-life-cycle](/notes/images/thread-life-cycle.png)

## Init
- Thread creation `thread_create()` puts a thread into its `init` state and allocates and initialises per-thread data structures.
- Once that is done, thread creation code puts the thread in `ready` state by adding the thread to the _ready list_ (set of runnable threads that are waiting their turn to use a processor).

## Ready
- A thread in `ready` state is available to be run but is not currently running.
- Its TCB is on the ready list, and the values of its registers are stored in its TCB.
- At any time, the **scheduler** can cause a thread to transition from `ready` to `running` state, by copying its register values from its TCB to a processor's registers.

## Running
- A thread in `running` state is running on a processor. At this time, its register values are stored on the processor rather than in the TCB.
- A `running` thread can transition to the `ready` state in two ways:
	- The **scheduler** can _preempt_ a `running` thread and move it to the `ready` state by saving the thread's registers to its TCB and switching the processor to run the next thread on the ready list.
	- A `running` thread can voluntarily relinquish the processor and go from `running` to `ready` by calling `thread_yield()`.

## Waiting
- A thread in the `waiting` state is waiting for some event.
- While the scheduler can move a thread in the `ready` state to the `running` state, a thread in the `waiting` state cannot run until some action by another thread moves it from `waiting` to `ready`.
- The TCB of a `waiting` thread is stored on the _waiting list_ of some synchronisation variable associated with the event. When the required event occurs, the operating system moves the TCB from the synchronisation variable's waiting list to the scheduler's ready list, transitioning the thread from `waiting` to `ready`.

## Finished
- A thread in `finished` state never runs again.
- The system can free some or all of its state for other use. Some systems may store `finished` threads in a _finished list_.


One way to understand the states is to consider where a thread's TCB and registers are stored.

| State of Thread | Location of TCB                            | Location of Registers |
| --------------- | ------------------------------------------ | --------------------- |
| `init`          | Being Created                              | TCB                   |
| `ready`         | Ready List                                 | TCB                   |
| `running`       | Running List                               | Processor             |
| `waiting`       | Waiting List of a Synchronisation Variable | TCB                   |
| `finished`      | Finished List / Deleted                    | TCB / Deleted         |

