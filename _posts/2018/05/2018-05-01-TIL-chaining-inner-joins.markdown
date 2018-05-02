---
layout: post
title:  "TIL: Chaining SQL Inner Joins"
date:   2018-05-01 20:15:00 -0000
categories: TIL
---
Short update for me today as I've been dealing with a deadly sinus headache all evening. I did get in some training this morning which covered the concept of chaining inner joins together using SQL queries. This gives the ability to join more than just two tables together, again using the primary and foreign key relationships between the two tables.

### The tables
Here are the three tables that I'll be using in my examples:
```sql
create table customers (cid serial primary key, cfirst char(50) not null);
insert into customers (cfirst) values ('Joe'), ('Jim'), ('Jane'), ('Juan');

 cid |                       cfirst                       
-----+----------------------------------------------------
   1 | Joe                                               
   2 | Jim                                               
   3 | Jane                                              
   4 | Juan                                              
```

```sql
create table movies (mid serial primary key, mmovie char(50) not null);
insert into movies (mmovie) values ('Die Hard'), ('American Beauty'), ('First Blood'), ('Cold Mountain'), ('Big Fish'), ('Alien');

 mid |                       mmovie                       
-----+----------------------------------------------------
   1 | Die Hard                                          
   2 | American Beauty                                   
   3 | First Blood                                       
   4 | Cold Mountain                                     
   5 | Big Fish                                          
   6 | Alien                                             
```

```sql
create table rentals (rid serial primary key, cid int references customers(cid), mid int references movies(mid));
insert into rentals (cid, mid) values (1, 3), (1, 2), (4, 5), (3, 6), (4, 4), (4, 2), (2, 3);

 rid | cid | mid 
-----+-----+-----
   1 |   1 |   3
   2 |   1 |   2
   3 |   4 |   5
   4 |   3 |   6
   5 |   4 |   4
   6 |   4 |   2
   7 |   2 |   3

```
With these three tables created, I can then chain together `inner join` commands to get the relation between all three tables:

```sql
select * from customers inner join rentals on customers.cid = rentals.cid inner join movies on movies.mid = rentals.mid;

 cid |                       cfirst                       | rid | cid | mid | mid |                       mmovie                       
-----+----------------------------------------------------+-----+-----+-----+-----+----------------------------------------------------
   1 | Joe                                                |   1 |   1 |   3 |   3 | First Blood                                       
   1 | Joe                                                |   2 |   1 |   2 |   2 | American Beauty                                   
   4 | Juan                                               |   3 |   4 |   5 |   5 | Big Fish                                          
   3 | Jane                                               |   4 |   3 |   6 |   6 | Alien                                             
   4 | Juan                                               |   5 |   4 |   4 |   4 | Cold Mountain                                     
   4 | Juan                                               |   6 |   4 |   2 |   2 | American Beauty                                   
   2 | Jim                                                |   7 |   2 |   3 |   3 | First Blood                                       
```

This is still pretty ugly though, as all of the tables contents are being shown. We can clean it up by putting in a bit of filtering:
```sql
select customers.cid, customers.cfirst, movies.mid, movies.mmovie from customers inner join rentals on customers.cid=rentals.cid inner join movies on movies.mid=rentals.mid;

 cid |                       cfirst                       | mid |                       mmovie                       
-----+----------------------------------------------------+-----+----------------------------------------------------
   1 | Joe                                                |   3 | First Blood                                       
   1 | Joe                                                |   2 | American Beauty                                   
   4 | Juan                                               |   5 | Big Fish                                          
   3 | Jane                                               |   6 | Alien                                             
   4 | Juan                                               |   4 | Cold Mountain                                     
   4 | Juan                                               |   2 | American Beauty                                   
   2 | Jim                                                |   3 | First Blood                                       
```

When doing the joining, it doesn't seem to matter what order that the keys come in, as long as you've got the primary and foreign key evaluating against one another. So the above query could be written in different ways and still be successful.

💚