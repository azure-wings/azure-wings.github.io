---
title: "Condition variable"
math: true
toc: true
---

## Definition
A **condition variable** is a synchronisation object that lets a [thread](notes/Thread.md) efficiently wait for a change to shared state that is protected by a [lock](notes/Lock.md).

## APIs
A condition variable has three methods.

- **`CV::wait(Lock *lock*)`**
	- This call [atomically](notes/Atomic%20operation.md) **releases the lock** and **suspends execution of the calling thread**, placing the calling thread on the condition variable's waiting list.
	- Later, when the calling thread is awakened, the lock is re-acquired before returning from the `wait` call.

- **`CV::signal()`**
	- This call takes **one** thread off the condition variable's wait list and marks it as eligible to run (i.e., it puts the thread on the scheduler's ready list).
	- If no threads are on the waiting list, `signal` has no effect.

- **`CV::broadcast()`**
	- This call takes **all** threads off the condition variable's waiting list and marks them as eligible to run.
	- If no threads are on the waiting list, `broadcast` has no effect.

## Properties
### Memoryless
- The conditional variable itself has _no internal state_ other than a **queue** of waiting threads.
	- Condition variables do not need their own state because they are always used inside shared objects that have their own state.
- If no threads are currently on the condition variable's waiting list, a `signal` or `broadcast` has no effect.
- The condition variable has no _memory_ of earlier calls to `signal` or `broadcast`.

### [Atomic](notes/Atomic%20operation.md)  Lock Release
- A thread always calls `wait` while holding a lock. The call to `wait` atomically releases the lock and puts the thread on the condition variable's waiting list.
	- Atomicity ensures that there is no separation between checking the shared object's state, deciding to wait, adding the waiting thread to the condition variable's queue and releasing the lock, so that some other thread can access the shared object.

### Non-immediate Return
- When a waiting thread is re-enabled, it is moved to the [scheduler](notes/Scheduler.md)'s ready queue with no special priority, and the scheduler may run it at some later time.
- Furthermore, when the thread finally does run, it must re-acquire the lock, which means that other threads may have acquired and released the lock in the meantime, between the `signal` / `broadcast` occurs and when the waiter re-acquires the lock.
- Even if the desired predicate were true when `signal` / `broadcast` was called, it may no longer be true when `wait` returns.