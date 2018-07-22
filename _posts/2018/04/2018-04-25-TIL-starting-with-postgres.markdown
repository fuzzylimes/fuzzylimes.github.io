---
layout: post
title:  "TIL: Starting with postgresql"
date:   2018-04-25 17:30:00 -0000
categories:
  - Coding
tags:
  - postgresql
---
As I mentioned in my last post, I wanted to get a bit more familiar with postgres before I started trying to work it into a project. Granted doing a project is a great way to learn something new, I felt like actually understanding how the db works before hand would be a bit better than going in completely blind.

So tonight I completed a few more lessons from the golang web tutorial that I'd been taking, as the course does have an entire section dedicated strictly to postgres. And the majority of the lesson is devoted to learning postgres, so that's an extra bonus for me!

Without retyping everything again, here are the notes for the areas I covered in my session today:

## Notes from 4/23
## Basic (baisc) postgres items
* `psql` - start postgres terminal (logs into default database)
* `psql <dbname>` - start postgres terminal in specific database
* `\l` - list all databases
* `\q` - exit the terminal
* `\d` - list all tables in selected database
* Make sure to end all commands with a `;` character
* You don't have to type commands in CAPSLOCK, lower case is fine
* You cannot delete a database that you are currently viewing (\c out of it first)

#### Create Database
```sql
CREATE DATABASE <database>;
```

#### Switch Database
```sql
\c <database name>
```

#### See current user
```sql
SELECT current_user;
```

#### See current database
```sql
SELECT current_database();
```

#### Delete Database
```sql
DROP DATABASE <database>;
```

#### Create a Table
* Use the command `CREATE TABLE <tablename`:
```sql
CREATE TABLE employees (
   ID INT PRIMARY KEY     NOT NULL,
   NAME           TEXT    NOT NULL,
   RANK           INT     NOT NULL,
   ADDRESS        CHAR(50),
   SALARY         REAL DEFAULT 25500.00,
   BDAY			  DATE DEFAULT '1900-01-01'
);
```

#### Show Tables in selected DB
```sql
\d

           List of relations
 Schema |   Name    | Type  |  Owner   
--------+-----------+-------+----------
 public | employees | table | postgres
```

#### Show details of a Table
```sql
\d <table name>

                      Table "public.employees"
 Column  |     Type      | Collation | Nullable |      Default       
---------+---------------+-----------+----------+--------------------
 id      | integer       |           | not null | 
 name    | text          |           | not null | 
 rank    | integer       |           | not null | 
 address | character(50) |           |          | 
 salary  | real          |           |          | 25500.00
 bday    | date          |           |          | '1900-01-01'::date
Indexes:
    "employees_pkey" PRIMARY KEY, btree (id)
```

#### Remove Table
```sql
DROP TABLE <table name>;
```

#### Insert Table Record
```sql
INSERT INTO employees (ID,NAME,RANK,ADDRESS,SALARY,BDAY) VALUES (1, 'Mark', 7, '1212 E. Lane, Someville, AK, 57483', 43000.00 ,'1992-01-13');
```

#### List all Table Records
```sql
SELECT * FROM <table name>;

 id | name | rank |                      address                       | salary |    bday    
----+------+------+----------------------------------------------------+--------+------------
  1 | Mark |    7 | 1212 E. Lane, Someville, AK, 57483                 |  43000 | 1992-01-13
(1 row)

```

#### Other Insert Examples
* Values that are not included will be added using [default values](https://www.postgresql.org/docs/9.3/static/ddl-default.html):
```sql
INSERT INTO employees (ID,NAME,RANK,ADDRESS,BDAY) VALUES (2, 'Marian', 8, '7214 Wonderlust Ave, Lost Lake, KS, 22897', '1989-11-21');

                      Table "public.employees"
 Column  |     Type      | Collation | Nullable |      Default       
---------+---------------+-----------+----------+--------------------
 salary  | real          |           |          | 25500.00

 id |  name  | rank |                      address                       | salary |    bday    
----+--------+------+----------------------------------------------------+--------+------------
  2 | Marian |    8 | 7214 Wonderlust Ave, Lost Lake, KS, 22897          |  25500 | 1989-11-21
  ```
* Inserting multiple rows at once:
```sql
INSERT INTO employees (ID,NAME,RANK,ADDRESS,SALARY,BDAY) VALUES (4, 'Jasmine', 5, '983 Star Ave., Brooklyn, NY, 00912 ', 55700.00, '1997-12-13' ), (5, 'Orranda', 9, '745 Hammer Lane, Hammerfield, Texas, 75839', 65350.00 , '1992-12-13');
```

#### Auto Increment Primary Key Field
* Done using either smallserial, serial or bigserial
```sql
CREATE TABLE phonenumbers(
	ID  SERIAL PRIMARY KEY,
	PHONE           TEXT      NOT NULL
);

INSERT INTO phonenumbers (PHONE) VALUES ( '234-432-5234'), ('543-534-6543'), ('312-123-5432');

\d phonenumbers;

SELECT * FROM phonenumbers;
```