---
title: "Thread models"
math: true
toc: true
---

Support for threads may be provided either at the user level, for **user threads**, or by the kernel, for **kernel threads**. **User threads** are supported above the kernel and are managed without kernel support, whereas **kernel threads** are supported and managed directly by the operating system. Accordingly, a _relationship_ must exist between user threads and kernel threads.

## One-to-one Model
![one-to-one-model](/notes/images/one-to-one-model.png)
The **one-to-one model** maps each user thread to a kernel thread.
|             |                                                                                                                                      |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Advantages  | Provides _more concurrency_ than the many-to-one model by allowing another thread to run when a thread makes a blocking system call. |
| Limitations | Every thread operation must go through the kernel; slower performance.                                                               |
|             | One-size fits all thread implementation; maybe pay for fancy features that a thread doesn't need.                                    |
|             | General heavy-weight memory requirements (e.g., requires a _fixed-size stack_ within kernel).                                        |
 
## Many-to-one Model
![many-to-one-model](/notes/images/many-to-one-model.png)

The **many-to-one model** maps many user-level threads to one kernel thread.
|             |                                                                                               |
| ----------- | --------------------------------------------------------------------------------------------- |
| Advantages  | Thread scheduling is done in user space, so it is efficient.                                  |
| Limitations | Can't take advantage of multicore systems.                                                    |
|             | User-level threads are invisible to the OS and thus not well-integrated with the OS.          |
|             | As a result, the OS can make poor decisions (e.g., a blocking system call blocks all threads) |

## Many-to-many Model
![many-to-many-model](/notes/images/many-to-many-model.png)

The **many-to-many model** multiplexes many user-level threads to a smaller or equal number of kernel threads. This is sometimes also called **n:m thread model**, where n is the number of user threads, and m is the number of kernel threads.