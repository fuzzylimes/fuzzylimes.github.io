---
layout: post
title:  "TIL: Starting with SQL Joins and URL encoding"
date:   2018-04-30 20:30:00 -0000
categories:
  - Coding
tags:
  - sql
---
Today's a mix of a few different things. I ran into an issue while running some tests at work involving unicode characters that led me down a hole regarding encoding. And after work I spent a bit more time on basic SQL stuff where I learned about doing two different types of joins.

### URI Encoding
So it turns out that you can't just send unicode characters through the URL. Even though you can type them into your browser using the characters, and even though your browser shows you those characters in the nav bar, that's not really what's being used. Turns out theres a different type of encoding that has to be used in order to send the address.

The situation that I ran into at work was regarding a specific resource that queries based on a user created string, such as a user name. Well, since it's possible that those user names will be created by people in different countries, and we have to support unicode for that, then my test lead me to trying to send a query using those characters. It looked like all of the internal servies were handling it just fine, but my query would constantly fail, like it had no idea what resource I was even looking for.

After some digging, I found out that the address needed to be translated over to using percent encoding. More info on that, as well as the process of converting the url, can be found on this [handy page](https://www.url-encode-decode.com/).

### SQL Joins
Tonight I learned about the first two kinds of table joins in SQL: `cross join` and `inner join`

Cross joins basically take all of the rows from two tables and create every combination of the records. So if you have 4 records in your first table, and 5 records in your second, you'll end up with 20 records. This doesn't seem to be very helpful to me right now, and I'm struggling to see a use case for it. But it's a thing that exists.

A `cross join` query looks something like this:
```
SELECT * FROM person CROSS JOIN sport;
```

And here's what a table using `cross join` looks like:
```sql
id |                        name                        | age | gender | id |                        name                        | pid 
----+----------------------------------------------------+-----+--------+----+----------------------------------------------------+-----
  1 | Bob                                                |  24 | M      |  1 | Surf                                               |   1
  2 | Jane                                               |  34 | F      |  1 | Surf                                               |   1
  3 | Jim                                                |  32 | M      |  1 | Surf                                               |   1
  4 | Li                                                 |  41 | F      |  1 | Surf                                               |   1
  1 | Bob                                                |  24 | M      |  2 | Skate                                              |   3
  2 | Jane                                               |  34 | F      |  2 | Skate                                              |   3
  3 | Jim                                                |  32 | M      |  2 | Skate                                              |   3
  4 | Li                                                 |  41 | F      |  2 | Skate                                              |   3
  1 | Bob                                                |  24 | M      |  3 | Run                                                |   3
  2 | Jane                                               |  34 | F      |  3 | Run                                                |   3
  3 | Jim                                                |  32 | M      |  3 | Run                                                |   3
  4 | Li                                                 |  41 | F      |  3 | Run                                                |   3
  1 | Bob                                                |  24 | M      |  4 | Bike                                               |   2
  2 | Jane                                               |  34 | F      |  4 | Bike                                               |   2
  3 | Jim                                                |  32 | M      |  4 | Bike                                               |   2
  4 | Li                                                 |  41 | F      |  4 | Bike                                               |   2
  1 | Bob                                                |  24 | M      |  5 | Row                                                |   1
  2 | Jane                                               |  34 | F      |  5 | Row                                                |   1
  3 | Jim                                                |  32 | M      |  5 | Row                                                |   1
  4 | Li                                                 |  41 | F      |  5 | Row                                                |   1
```

Inner joins appear to be much much more useful. This allows you to compare data between two different tables based on primary and foreign keys. This way you can get all of the matching data for a user between tables, and pair it down as you want.

Here's what an `inner join` would look like (very, very simple):
```
select * from person inner join sport on person.id = sport.pid;
```

And this is what the `inner join` query above would return:
```
 id |                        name                        | age | gender | id |                        name                        | pid 
----+----------------------------------------------------+-----+--------+----+----------------------------------------------------+-----
  1 | Bob                                                |  24 | M      |  1 | Surf                                               |   1
  3 | Jim                                                |  32 | M      |  2 | Skate                                              |   3
  3 | Jim                                                |  32 | M      |  3 | Run                                                |   3
  2 | Jane                                               |  34 | F      |  4 | Bike                                               |   2
  1 | Bob                                                |  24 | M      |  5 | Row                                                |   1
```

💚