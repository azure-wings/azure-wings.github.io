---
title: "Structure of relational databases"
math: true
toc: true
---

A relational database consists of a collection of **tables**, each of which is assigned a unique name.
In general, a row in a table represents a *relationship* among a set of values.

- In the relational model, the term **relation** is used to refer to a table, whilst the term **tuple** is used to refer to a row.
- Similarly, the term **attribute** refers to a column of a table.
    - Denoted as $A_1, \cdots, A_n$.
        
        ![Screenshot 2022-10-10 at 6.53.06 PM.png](Structure%20of%20Relational%20Databases%209c04c2584af142379f668c5078a9d46d/Screenshot_2022-10-10_at_6.53.06_PM.png)
        
- A **relation schema** consists of a list of attributes and their corresponding domains.
    - Denoted as $R = (A_1, \cdots, A_n)$.
- The term **relation instance** refers to a specific instance of a relation, i.e., containing a specific set of rows.
    - Denoted as $r(R)$.
- The **domain** of the attribute refers to the set of allowed values for each attribute.
    - Attribute values are normally required to be **atomic**, i.e., elements of the domain are considered to be indivisible unit**s**.
    - The special value **null** is a member of every domain, indicating that the value is *unknown*.
- Relations are unordered, like sets in mathematics.