---
title: "Recursive queries"
math: true
toc: true
---

Recursive [[notes/Views | views]] make it possible to write queries that cannot be written without recursion or iteration.

**Example**
- Find all (direct or indirect) prerequisite subjects of each course
```sql
WITH RECURSIVE rec_prereq(course_id, prereq_id) AS
(
    (
        SELECT  course_id,
            prereq_id
        FROM    prereq
    )
    UNION
    (
        SELECT  rec_prereq.course_id,
            prereq.prereq_id
        FROM    rec_prereq,
                prereq
        WHERE   rec_prereq.prereq_id = prereq.course_id
    )
)
SELECT  course_id
FROM    rec_prereq;
```
The example view `rec_prereq` is called the **transitive closure** of the `prereq` relation, meaning that it is a relation that contains all pairs (`cid`, `pre`) such that `pre` is a direct or indirect prerequisite of `cid`.

Recursive views are required to be **monotonic**.
- For each step of the recursion, the view **must** contain all of the tuples it contained in the previous step, plus possibly some more.

- At some point, no tuple is added to the view after recursion. This final result is called the **fixed point** of the recursive view definition.