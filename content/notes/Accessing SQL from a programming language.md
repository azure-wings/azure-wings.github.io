---
title: "Accessing SQL from a programming language"
math: true
toc: true
---

A database programmer must have access to a general purpose programming language for at least two reasons:
- Not all queries can be expressed in SQL.
  
  SQL does not provide the full expressive power of a general-purpose language

- Non-declarative actions cannot be done from within SQL.
  
  Non-delcatarive actions include printing a report, interacting with a user, and sending the results of a query to a GUI.

There are two approaches to accessing SQL from a general purpose programming language:
- **Dynamic SQL**
  
  A general purpose program can _connect to_ and _communicate with_ a database server using a collection of functions.

- **Embedded SQL**
  
  Provides a means by which program can interact with a database server. However, under embedded SQL:
  - The SQL statements are identified at compile time, and are translated into function calls.
  
  - At runtime, these function calls connect to the database using an API that provides dynamic SQL facilities (but may be specific to the database being used).