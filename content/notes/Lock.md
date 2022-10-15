---
title: "Lock"
math: true
toc: true
---

## Definition
A **lock** is a synchronisation variable that provides **mutual exclusion** - when one thread holds a lock, no other thread can hold it.

## APIs
A lock enables mutual exclusion by providing two methods: `Lock::acquire()` and `Lock::release()`. These methods are defined as follows:

- A lock can be in one of two states: `busy` or `free`.
- A lock is initially in the `free` state.
- **`Lock::acquire()`**
	- The caller thread **waits** until the lock is `free` and then atomically makes the lock `busy`.
	- Checking the state of a lock and setting the state to `busy` are, together, an [atomic operation](notes/Atomic%20operation.md).
	- Even if multiple threads try to acquire the lock, at most one thread will succeed.
- **`Lock::release()`** 
	- This call makes the lock `free`.
	- If there are pending `acquire()` operations, this state change causes one of them to proceed.

## Properties
A lock should ensure the three properties: **mutual exclusion**, **progress**, and **bounded waiting**. Mutual exclusion ensures [safety](notes/Too%20much%20milk%20problem###Safety), while progress and bounded waiting ensures [liveliness](notes/Too%20much%20milk%20problem###Liveliness).

### Mutual Exclusion
At most **one** thread can hold the lock.

### Progress
If no thread holds the lock and any thread attempts to acquire the lock, then eventually some thread succeeds in acquiring the lock.

### Bounded Waiting
If a thread $T$ attempts to acquire a lock, then there exists a bound on the number of times other threads can successfully acquire the lock before $T$ does.

## Rules for Using Locks
- **Lock is initially free**.
- **Always acquire lock before accessing shared data.
- **Always release after finishing with shared data**.
- **Never access shared data without acquiring lock**.
