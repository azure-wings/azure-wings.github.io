---
title: "Bounded buffer problem"
math: true
toc: true
---

## Definition
```
+----------+                    +----------+
|          |    +----------+    |          |
| Producer |--->|  Buffer  |--->| Consumer |
|          |    +----------+    |          |
+----------+                    +----------+
```

- The producer puts objects into a shared buffer.
- The consumer takes them out.
- There must be a synchronisation to coordinate between the producer and the consumer.
- The producer and the consumer should not need to work in [lock](Lock.md) step; there is a fixed-size buffer between them.
	- The access to this buffer must be synchronised.
	- The producer must wait if the buffer is full.
	- The consumer must wait if the buffer is empty.

## Implementation Example
- **Producer**
```C
for (int i = 0; i<MAX_LOOP; i++)
{
  try_put (i);
}
```

- **Consumer**
```C
while (true)
{
  int tmp = try_get ();
  printf ("%d\n", tmp);
}
```

Initially, the buffer is a _queue_ with `front = tail = 0`, and the lock is initially `free`. Let `MAX` be the maximum capacity of the buffer. Then, the `try_put ()` and `try_get ()` can be implemented as follows.

- **`try_put`**
```C
try_put (item)
{
  lock.acquire ();
  if ((tail - front) < size)    // Buffer is not full
  {
	buffer[tail % MAX] = item;
	tail++;
  }
  lock.release ();
}
```

- **`try_get`**
```C
try_get ()
{
  item = NULL;
  lock_acquire ();
  if (front < tail)            // Buffer is not empty
  {
	item = buffer[front % MAX];
	front++;
  }
  lock_release ();
  return item;
}
```

Here, the shared states are `buffer`, `front`, and `tail`.

However, one cannot assure that the `buffer` is empty when `try_get ()` returns `NULL`.
- If a producer generates an item between `lock_release ()` and `return`, even though the `buffer` is not empty, `try_get ()` returns `NULL`.
- For a thread to know when the `buffer` is empty, there must be _[another primitive](Condition%20variable.md)_ for the purpose.