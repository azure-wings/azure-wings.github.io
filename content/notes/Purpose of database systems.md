---
title: "Purpose of database systems"
math: true
toc: true
---

In the early days, [database](notes/Database%20systems.md) applications were built directly on top of file systems, which leads to several disadvantages.

- **Data redundancy and inconsistency**
  
  Data is stored in multiple file formats, resulting in duplication of information in different files. In addition, this may lead to data inconsistency, where the various copies of the same data no longer agree.

- **Difficulty in accessing data**
  
  Conventional file-processing environments do not allow needed data to be retrieved in a convenient and efficient manner.

- **Data isolation**
  
  Because data are scattered in _various files_, and files may be in _different formats_, writing new application programs to retrieve the appropriate data is difficult.

- **Integrity problems**

    The data values stored in the database must satisfy certain types of _integrity constraints_(e.g., `account_balance >= 0`). Without database systems, these integrity constraints become buried in the program code, making it hard to add new constrains or change existing ones.

- **Atomicity problems**

    Failures may leave data in an inconsistent state with only partial updates carried out; data update must be _[atomic](notes/Atomic%20operation.md)_. It is difficult to ensure atomicity in a conventional file-processing system.

- **Concurrent access anomalies**
  
  For the sake of overall performance, many systems allow concurrent access to data. However, uncontrolled concurrent access can lead to data inconsistencies.

- **Security problems**
  
  Not every user of the database system should be able to access all the data. It is hard to provide user access to som, but not all, data in conventional file-processing environments.

[[notes/Database systems]] offer solutions to all of the above problems.