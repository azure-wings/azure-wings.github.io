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
TO      <user list>
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
- A **role**

Note that
- Granting a privilege on a view does **not** imply granting any privileges on the underlying relations.
  
- The grantor of the privilege **must** already hold the privilege on the specified item.

### `REVOKE` statement
The `REVOKE` statement is used to **revoke** authorisation.
```sql
REVOKE  <privilege list>
ON      <relation / view>
TO      <user list>
```
If the `<privilege list>` is
- `ALL`: **All** privileges the revokee may hold, are revoked.

If the `<user list>` is 
- `PUBLIC`: **All** users lose the privilege, except those granted it explicitly.

Note that
- If the same privilege was granted more than once to the same user by **different** grantees, then the user may **retain** the privilege after one revocation.

- All privileges that depend on the privilege being revoked are **also revoked**.