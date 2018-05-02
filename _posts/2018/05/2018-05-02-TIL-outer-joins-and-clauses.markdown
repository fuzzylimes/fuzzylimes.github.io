---
layout: post
title:  "TIL: SQL Outer Joins and Clauses"
date:   2018-05-02 18:30:00 -0000
categories: TIL
---
Today wrapped up the lessons on joining tables and went a bit further into working with clauses (help greatly with writing useful filters). All of this is going to be copy and pasted from my notes for the day, so lets just get into it.

### Outer Joins
* Outer joins will give you all of the items in tables, even if they aren't related to an item in the other.
* For instance if you have a table of sports, and not all sports are tied to a specific person, the outer join could show you either all of the people, regardless if they're related to a sport, or all of the sports, regardless if they're related to a person.
* There are three types of `outer join` queries that can be done:
    * `left outer join`
    * `right outer join`
    * `full outer join`
* For the first two, what is returned depends on the order of the tables being joined in the command.
* The syntax for the outer join is `select <filter> from <table1> <outer join type> <table2> on <p.key>=<f.key>;`
* In the `left` or `right` commands will be based on whatever tables are present in the `<table1>` and `<table2>` fields above.

Here are the two tables I'll be working with:
```sql
select * from person;

 id |                        name                        | age | gender 
----+----------------------------------------------------+-----+--------
  1 | Bob                                                |  24 | M 
  2 | Jane                                               |  34 | F 
  3 | Jim                                                |  32 | M 
  4 | Li                                                 |  41 | F 
```

```sql
select * from sport;

 id |                        name                        | pid 
----+----------------------------------------------------+-----
  1 | Surf                                               |   1
  2 | Skate                                              |   3
  3 | Run                                                |   3
  4 | Bike                                               |   2
  5 | Row                                                |   1
```

#### left outer join
* Based on the positioning of tables in the query like mentioned before.
* Will use the first table as the table from which to pull everything and join with table2 items.
* To get all of the people, and sports they're related to:
```sql
select person.name, sport.name from person left outer join sport on person.id=sport.pid;

                        name                        |                        name                        
----------------------------------------------------+----------------------------------------------------
 Bob                                                | Surf                                              
 Jim                                                | Skate                                             
 Jim                                                | Run                                               
 Jane                                               | Bike                                              
 Bob                                                | Row                                               
 Li                                                 | 
```
* Or to get all of the sports and the people they're related to:
```sql
select person.name, sport.name from sport left outer join person on sport.pid=person.id;
                        name                        |                        name                        
----------------------------------------------------+----------------------------------------------------
 Bob                                                | Surf                                              
 Jim                                                | Skate                                             
 Jim                                                | Run                                               
 Jane                                               | Bike                                              
 Bob                                                | Row                                               
                                                    | Bowling                       
```

#### right outer join
* Basically the reverse of the left outer join, this uses the second table in the query to be queried from.
* So we can repeat the same thing that was done in the first example above by flipping the query around:
```sql
select person.name, sport.name from sport right outer join person on sport.pid=person.id;
```
* Or the second:
```sql
select person.name,sport.name from person right outer join sport on person.id=sport.id;
```

#### full outer join
* The full outer join will grab all items from both lists, inclduing both those that match and those that don't
```sql
select person.*, sport.name from sport full outer join person on sport.pid=person.id;
```

## Clauses
* Used to help pair down and bettery query for data
* Clauses:
    * `where`
    * `and`
    * `or`
    * `in`
    * `not`
    * `between`
    * `is not null`
    * `like`
    * `limit`
    * `order by`

Starting with the following table:
```sql
select * from employees;

 id |  name   | rank |                      address                       | salary |    bday    
----+---------+------+----------------------------------------------------+--------+------------
  1 | Mark    |    7 | 1212 E. Lane, Someville, AK, 57483                 |  43000 | 1992-01-13
  2 | Marian  |    8 | 7214 Wonderlust Ave, Lost Lake, KS, 22897          |  25500 | 1989-11-21
  4 | Jasmine |    5 | 983 Star Ave., Brooklyn, NY, 00912                 |  55700 | 1997-12-13
  5 | Orranda |    9 | 745 Hammer Lane, Hammerfield, Texas, 75839         |  65350 | 1992-12-13
  3 | Maxwell |    6 | 7215 Jasmine Place, Corinda, CA 98743              |  87500 | 1900-01-01
```

### WHERE
```sql
select * from employees where salary > 60000;

 id |  name   | rank |                      address                       | salary |    bday    
----+---------+------+----------------------------------------------------+--------+------------
  5 | Orranda |    9 | 745 Hammer Lane, Hammerfield, Texas, 75839         |  65350 | 1992-12-13
  3 | Maxwell |    6 | 7215 Jasmine Place, Corinda, CA 98743              |  87500 | 1900-01-01
```

### AND
```sql
select * from employees where salary > 60000 and rank > 7;

 id |  name   | rank |                      address                       | salary |    bday    
----+---------+------+----------------------------------------------------+--------+------------
  5 | Orranda |    9 | 745 Hammer Lane, Hammerfield, Texas, 75839         |  65350 | 1992-12-13
```

### OR
```sql
select * from employees where salary > 60000 or rank > 7;

 id |  name   | rank |                      address                       | salary |    bday    
----+---------+------+----------------------------------------------------+--------+------------
  2 | Marian  |    8 | 7214 Wonderlust Ave, Lost Lake, KS, 22897          |  25500 | 1989-11-21
  5 | Orranda |    9 | 745 Hammer Lane, Hammerfield, Texas, 75839         |  65350 | 1992-12-13
  3 | Maxwell |    6 | 7215 Jasmine Place, Corinda, CA 98743              |  87500 | 1900-01-01
```

### IN
```sql
select * from employees where rank in (1,4,6,8);

 id |  name   | rank |                      address                       | salary |    bday    
----+---------+------+----------------------------------------------------+--------+------------
  2 | Marian  |    8 | 7214 Wonderlust Ave, Lost Lake, KS, 22897          |  25500 | 1989-11-21
  3 | Maxwell |    6 | 7215 Jasmine Place, Corinda, CA 98743              |  87500 | 1900-01-01
```

### NOT
```sql
select * from employees where rank not in (1,4,6,8);

 id |  name   | rank |                      address                       | salary |    bday    
----+---------+------+----------------------------------------------------+--------+------------
  1 | Mark    |    7 | 1212 E. Lane, Someville, AK, 57483                 |  43000 | 1992-01-13
  4 | Jasmine |    5 | 983 Star Ave., Brooklyn, NY, 00912                 |  55700 | 1997-12-13
  5 | Orranda |    9 | 745 Hammer Lane, Hammerfield, Texas, 75839         |  65350 | 1992-12-13
```

### BETWEEN
```sql
select * from employees where rank between 3 and 7 or salary between 40000 and 80000;

 id |  name   | rank |                      address                       | salary |    bday    
----+---------+------+----------------------------------------------------+--------+------------
  1 | Mark    |    7 | 1212 E. Lane, Someville, AK, 57483                 |  43000 | 1992-01-13
  4 | Jasmine |    5 | 983 Star Ave., Brooklyn, NY, 00912                 |  55700 | 1997-12-13
  5 | Orranda |    9 | 745 Hammer Lane, Hammerfield, Texas, 75839         |  65350 | 1992-12-13
  3 | Maxwell |    6 | 7215 Jasmine Place, Corinda, CA 98743              |  87500 | 1900-01-01
```

### IS NOT NULL
```sql
select * from employees where bday is not null;

 id |  name   | rank |                      address                       | salary |    bday    
----+---------+------+----------------------------------------------------+--------+------------
  1 | Mark    |    7 | 1212 E. Lane, Someville, AK, 57483                 |  43000 | 1992-01-13
  2 | Marian  |    8 | 7214 Wonderlust Ave, Lost Lake, KS, 22897          |  25500 | 1989-11-21
  4 | Jasmine |    5 | 983 Star Ave., Brooklyn, NY, 00912                 |  55700 | 1997-12-13
  5 | Orranda |    9 | 745 Hammer Lane, Hammerfield, Texas, 75839         |  65350 | 1992-12-13
  3 | Maxwell |    6 | 7215 Jasmine Place, Corinda, CA 98743              |  87500 | 1900-01-01
```

### LIKE
```sql
select * from employees where name like '%Ma%';

 id |  name   | rank |                      address                       | salary |    bday    
----+---------+------+----------------------------------------------------+--------+------------
  1 | Mark    |    7 | 1212 E. Lane, Someville, AK, 57483                 |  43000 | 1992-01-13
  2 | Marian  |    8 | 7214 Wonderlust Ave, Lost Lake, KS, 22897          |  25500 | 1989-11-21
  3 | Maxwell |    6 | 7215 Jasmine Place, Corinda, CA 98743              |  87500 | 1900-01-01
```

### LIMIT
```sql
select * from employees limit 1;

 id | name | rank |                      address                       | salary |    bday    
----+------+------+----------------------------------------------------+--------+------------
  1 | Mark |    7 | 1212 E. Lane, Someville, AK, 57483                 |  43000 | 1992-01-13
```

### ORDER BY
```sql
select * from employees order by rank;

 id |  name   | rank |                      address                       | salary |    bday    
----+---------+------+----------------------------------------------------+--------+------------
  4 | Jasmine |    5 | 983 Star Ave., Brooklyn, NY, 00912                 |  55700 | 1997-12-13
  3 | Maxwell |    6 | 7215 Jasmine Place, Corinda, CA 98743              |  87500 | 1900-01-01
  1 | Mark    |    7 | 1212 E. Lane, Someville, AK, 57483                 |  43000 | 1992-01-13
  2 | Marian  |    8 | 7214 Wonderlust Ave, Lost Lake, KS, 22897          |  25500 | 1989-11-21
  5 | Orranda |    9 | 745 Hammer Lane, Hammerfield, Texas, 75839         |  65350 | 1992-12-13
```

💚