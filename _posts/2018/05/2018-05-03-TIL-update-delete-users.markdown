---
layout: post
title:  "TIL: SQL Updates and Deletes and Postgres User Management"
date:   2018-05-03 18:25:00 -0000
categories:
  - Coding
tags:
  - sql
---
More postgresql today. Today I learned about updating records, deleting records, and then how to create and manage users within postgres. Like yesterday, all of this is coming from the notes I took while working through it.

## Update Record
* To update a record, you need to make sure that you use a where clause to specify an exact record, otherwise EVERY record is going to be updated.
* Update syntax: `update <table> set <col1> = <val1> where <condition>;`

```sql
update employees set salary = 26000 where id=2;
```

## Delete Record
* Just like update, need to ensure that we use the where clause to specify exact record, or everything will be deleted!
* Delete syntax: `delete from <table> where <condition>;`

```sql
delete from sports where id=6;
```

## User Management
#### Details of users

```sql
\du

                                   List of roles
 Role name |                         Attributes                         | Member of 
-----------+------------------------------------------------------------+-----------
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}

```

#### Create User

```sql
create user bob with password 'password';

 Role name |                         Attributes                         | Member of 
-----------+------------------------------------------------------------+-----------
 bob       |                                                            | {}
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
```

#### Grant Privileges
privileges: SELECT, INSERT, UPDATE, DELETE, RULE, ALL

```sql
grant all privileges on database company to bob;

\l

                                  List of databases
    Name     |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges   
-------------+----------+----------+------------+------------+-----------------------
 blockbuster | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
 company     | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =Tc/postgres         +
             |          |          |            |            | postgres=CTc/postgres+
             |          |          |            |            | bob=CTc/postgres
```

#### Revoke Privileges
* grant privileges on different _databases_.

```sql
revoke all privileges on database company from bob;
```

#### Alter
* changes a users _roles_.

```sql
alter user bob with superuser;

\du

                                   List of roles
 Role name |                         Attributes                         | Member of 
-----------+------------------------------------------------------------+-----------
 bob       | Superuser                                                  | {}
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
```

#### Remove User

```sql
drop user bob;
```

💚