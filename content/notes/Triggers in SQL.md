---
title: "Triggers in SQL"
math: true
toc: true
---

A **trigger** is a statement that is executed automatically by the system as a side effect of a modification to the database.

The two requirements of a trigger design are:
- Specify the **conditions** under which the trigger is to be execute.
- Specify the **actions** to be taken when the trigger executes.

## Triggering events and actions in SQL
- Triggering event can be an insert, a deletion, or an update.

- Triggers on updates can be restricted to specific attributes.

- Values of attributes before and after an update can be referenced.
  - `REFERENCING OLD ROW AS`: For deletions and updates
  - `REFERENCING NEW ROW AS`: For insertions and updates

- Triggers can be activated before and after an event.
  - `BEFORE UPDATE OF`: Serves as an extra constraint.
  - `AFTER UPDATE OF`

**Examples**
- When the `grade` attribute is updated for a tuple in the `takes` relation, keep the `tot_cred` attribute value of `student` tuples up-to-date
```sql
-- When (Trigger Conditions)
CREATE TRIGGER credits_earned
AFTER UPDATE OF takes ON (grade)
-- What (Trigger Actions)
REFERENCING NEW ROW AS nrow
REFERENCING OLD ROW AS orow
FOR EACH ROW
WHEN    (nrow.grade <> 'F' AND nrow.grade IS NOT NULL)
AND     (orow.grade = 'F'  OR  orow.grade IS NULL)
BEGIN ATOMIC
    UPDATE  student
    SET     tot_cred = tot_cred +
    (
        SELECT  credits
        FROM    course
        WHERE   course.course_id = nrow.course_id
    )
    WHERE   student.id = nrow.id;
END;
```

### Statement level triggers
Instead of executing a separate action for each affected row, a single action can be executed for all rows affected by a transaction.
- Instead of `FOR EACH ROW`, use `FOR EACH STATEMENT`.

- Instead of `REFERENCING [OLD/NEW] ROW AS ...`, use `REFERENCING [OLD/NEW] TABLE AS ...` to refer to temporary tables (called **transition tables**).

Statement level triggers can be more efficient when dealing with SQL statements that update a large number of rows.

## When not to use triggers
Earlier, triggers were used for tasks such as
- Maintaining **summary data**.

- Replicating databases by recording changes to special relations (called **change** or **delta** relations), and having a separate process that applies the changes over to a replica

However, there are better ways of doing these nowadays.
- Databases today provide built-in [[notes/Views#Materialised views | materialised view]] facilities to maintain summary data.

- Databases provide built-in support for replication.

- Encapsulation facilities can be used instead of triggers in many cases. It carries out actions as part of the update methods instead of through a trigger.

### Risks of using triggers
There are some risks for using triggers. For example,
- Risk of unintended execution of triggers.

- Error leading to failure of critical transactions that set off the trigger.

- Cascading execution of triggers.