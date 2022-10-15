---
title: "Comparison between processes and threads"
math: true
toc: true
---

## Comparison
|                        | [Processes](notes/Process.md)                 | [Threads](notes/Thread.md)                                                    |
| ---------------------- | ------------------------------------------- | --------------------------------------------------------------------------- |
| Switch Overhead        | High (CPU state + Memory, I/O state)        | Low (CPU state only)                                                        |
| Creation Cost          | High                                        | Low                                                                         |
| CPU Protection         | Yes                                         | Yes                                                                         |
| Memory, I/O Protection | Yes                                         | No                                                                          |
| Sharing Overhead       | High (Involves at leas a context switch)    | Low (Because thread switch overhead is low; may not need to switch context) |
| Sharing Security       | High (One process cannot corrupt the other) | Low (A thread can write the memory used by another thread)                  |

## Diagrams
![process-diagram](/notes/images/process-diagram.png)

![processes-diagram](/notes/images/processes-diagram.png)

![threads-diagram](/notes/images/threads-diagram.png)

