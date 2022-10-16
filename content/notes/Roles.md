---
title: "Roles"
math: true
toc: true
---

A **role** is a way to distinguish among various as far as what these users can access / update in the database.

A role can be thought of as a _set of [[notes/Authorisation | privileges]]_; with roles, privileges of multiple users can be managed at once.

Roles can be created as following.
```sql
CREATE ROLE <name>
```
Once a role is created, users can be assigned to the role as following.
```sql
GRANT   <role>
TO      <user list>
```
Note that
- Privileges can be granted to roles.
- Roles can be granted to users, as well as to other roles.