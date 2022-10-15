---
title: "Too much milk problem"
math: true
toc: true
---

## Definition
The **Too Much Milk** problem models two roommates who share a refrigerator and, who make sure the refrigerator is _always_ well stocked with milk.

## Example Situation
| Time | Roommate 1                   | Roommate 2                   |
| ---- | ---------------------------- | ---------------------------- |
| 3:00 | Look in fridge; out of milk. |                              |
| 3:05 | Leave for store.             |                              |
| 3:10 | Arrive at store.             | Look in fridge; out of milk. |
| 3:15 | Buy milk.                    | Leave for store.             |
| 3:20 | Arrive home; put milk away.  | Arrive at store.             |
| 3:25 |                              | Buy milk.                    |
| 3:30 |                              | Arrive home; put milk away.  |
|      |                              | **Oh no, too much milk!**    |

One can model each roommate as a **thread** and the number of bottles of milk in the fridge with **a variable in memory**. Two properties needs to be met for a solution: **safety** and **liveliness**.

### Safety
A program never enters a bad state.
- In the too much milk problem, never more than one person buys a milk.

### Liveliness
A program must, eventually, enter a good state.
- In the too much milk problem, if milk is needed, someone eventually buys it.

## Solutions
### Solution 1: Leave a note
The basic idea is to leave a note on the fridge before going to the store. The simplest idea to implement this is to set a flag when going to buy milk and to check this flag before going to buy milk.

```C
if(milk == 0)   // If no milk
{
  if(!note)     // If no note
  {
    leave note;
    buy milk;
    remove note;
  }
}
```

However, this implementation can violate safety; it makes the problem worse since it fails intermittenly!

| Thread A         | Thread B         |
| ---------------- | ---------------- |
| `if (milk == 0)` |                  |
| `if (note == 0)` |                  |
| _Interleaves_    | `if (milk == 0)` |
|                  | `if (note == 0)` |
| `note = 1;`      | _Interleaves_    |
| `milk++;`        |                  |
| `note = 0;`      |                  |
| _Interleaves_    | `note = 1;`      |
|                  | `milk++;`        |
|                  | `note = 0;`      |

### Solution 2: Using two notes
- Thread A
```C
leave note A;
if(!note B)
{
  if(milk == 0)
	buy milk;
}
remove note A;
```
- Thread B
```C
leave note B;
if(!note A)
{
  if(milk == 0)
	buy milk;
}
remove note B;
```

This solution is **safe**. However, this solution does not ensure **liveliness**. Although it is unlikely to happen, but it is possible at worst case.

| Thread A              | Thread B              |
| --------------------- | --------------------- |
| `leave note A`        |                       |
| _Interleaves_         | `leave note B`        |
|                       | `if (!note A)`        |
|                       | (PASS) `if (milk == 0)` |
|                       | (PASS) `buy milk`       |
| `if (!note B)`        | _Interleaves_         |
| (PASS) `if (milk == 0)` |                       |
| (PASS) `buy milk`       |                       |


### Solution 3: Busy waiting
- Thread A
```C
leave note A;
while(note B)
  ;
if(milk == 0)
  buy milk;
remove note A;
```

- Thread B
```C
leave note B;
if(!note A)
{
  if(milk == 0)
    buy milk;
}
remove note B;
```

This solution is both **safe** and **live**. Since thread B does not have a loop, it will eventually finish its execution.

However, this solution is not very satisfying:

- It is complex and requires caregul reasoning to be convinced that it works.
- It is _inefficient_ because thread A is _busy waiting_, consuming CPU resources.
- It may fail if the compiler or hardware reorders instructions.

### Solution 4: [Locks](Lock.md)
```C
lock.acquire();
if(milk == 0)
  buy milk;
lock.release();
```
