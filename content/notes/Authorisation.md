---
title: "Authorisation"
math: true
toc: true
---

A user can be assigned several forms of authorisations on parts of the database:
- **Read**
  
  Allows reading, but not modification of data

- **Insert**
  
  Allows insertion of new data, but not modification of existing data

- **Update**
  
  Allows modification, but not deletion of data

- **Delete**
  
  Allows deletion of data

Each of these types of authorisations is called **privilege**.

A user can be authorised all, none, or a combination of these types of privileges on specified parts of a database, such as a relation or a view.

## Granting and revoking or privileges
### `GRANT` statement
The `GRANT` statement is used to **confer** authorisation.
```sql
GRANT   <privilege list>
ON      <relation / view>
TO      <user list>;
```
Here, `<privilege list>` can be
- `SELECT`: Allows read access, or the ability query using the view
- `INSERT`: Ability to insert tuples
- `UPDATE`: Ability to update using the SQL `UPDATE` statement
- `DELETE`: Ability to delete tuples
- `ALL PRIVILEGES`: Short form for all the allowable privileges

and the `<user list>` can be
- a user ID
- `PUBLIC`, which allows all valid users the privilege granted
- A **[[notes/Roles | role]]**

Note that
- Granting a privilege on a view does **not** imply granting any privileges on the underlying relations.
  
- The grantor of the privilege **must** already hold the privilege on the specified item.

### `REVOKE` statement
The `REVOKE` statement is used to **revoke** authorisation.
```sql
REVOKE  <privilege list>
ON      <relation / view>
TO      <user list>;
```
If the `<privilege list>` is
- `ALL`: **All** privileges the revokee may hold, are revoked.

If the `<user list>` is 
- `PUBLIC`: **All** users lose the privilege, except those granted it explicitly.

Note that
- If the same privilege was granted more than once to the same user by **different** grantees, then the user may **retain** the privilege after one revocation.

- All privileges that depend on the privilege being revoked are **also revoked**.

## Authorisation on views
- A user who creates a [[notes/Views | view]] must have at least `SELECT` privilege on the base relation.
  
- The creator of the view does **not** receive all privileges on that view.
  - Only those privileges that provide no additional authorisation beyond those that the user already had, are given.
  
- Users who received only the privilege on the view does not have privilege on the base relation.

## Other authorisation features
### `REFERENCES` privilege
SQL includes a `REFERENCES` privilege that permits a user to declare foreign keys when creating relations.
```sql
GRANT   REFERENCES(A_1, ... , A_k)
ON      r
TO      <user list>;
```
- `r`: Relation
- `A_i`: Attributes of `r`

Such privilege is required because:
- [[notes/Integrity constraints#Referential integrity | Foreign key constraints]] restrict deletion and update operations on the referenced relation, which may restrict future activity by other users.

- With the `REFERENCES` privilege, the user can **check for the existence** of a certain value in a certain (set of) attributes of the referenced relation.

### Transfer of privileges
The privilege to allow the recipient to _pass the privilege onto other users_ can be explicitly given.
```sql
GRANT   <privilege list>
ON      <relation / view>
TO      <user list>
WITH GRANT OPTION;
```
It is also possible to specify the actions when a privilege is _revoked_ from a user.

One option is to **cascade** the revoking operation, meaning that **all** privileges the revokee granted with `GRANT OPTION` is also revoked.
```sql
REVOKE  <privilege list>
ON      <relation / view>
FROM    <user list>
CASCADE;
```
The keyword `CASCADE` can be omitted, as it is the basic behaviour of the `REVOKE` operation.

Another option is to maintain the privileges the revokee granted to other users, and only revoke the revokee's privilege.
```sql
REVOKE  <privilege list>
ON      <relation / view>
FROM    <user list>
RESTRICT;
```