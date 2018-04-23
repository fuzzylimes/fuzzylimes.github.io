---
layout: post
title:  "TIL: Standing up a Postgresql server in docker"
date:   2018-04-23 19:30:00 -0000
categories: TIL
---
The next project I have planned to goof off with deals with handling user authentication and authorization in a REST api. At the same time, I want to give an sql database a try as all I've really ever worked with is mongodb. I'd heard great things about postgres, so I figured I'd give that a go. And rather than installing it to my local computer, I decided I'd put my docker training to use and stand it up that way.

## docker-compose.yaml
There's nothing really special about the docker-compose.yaml file. I was able to get the first part of this from my sample notes that I'd taken during the lectures.

For my first start, I had something like this:
```yaml
version: '2'

services:
    postgres:
        image: postgres
        environment:
            POSTGRES_PASSWORD: example
```
After creating the file, I ran the `docker-compose up -d` command to stand up the container. I then fumbled around for the next 10 minutes trying to remember how to get into the container (FYI, it's `docker container exec -it <id> /bin/bash) so that I could create my new db name.

Once inside the container, I found that I couldn't do anything as root, I had to switch over to postgres user, from which I could then run a `createdb` to create a new database and then run `psql <db>` to get into the db shell.

From there I was able to create a new table and all that good stuff. At that point I wanted to check to see if my data would persist. So I tore down the session with `docker-compose down` and then restarted with `docker-compost up -d`.

It didn't stick around

## Second version of docker-compose.yaml
Okay, so I do need to do something with volumes to get the data to stick around. Back to the docker-compose file:

```yaml
version: '2'

services:
    postgres:
        image: postgres
        environment:
            POSTGRES_PASSWORD: example
            POSTGRES_DB: mydb
        volumes:
            - psql:/var/lib/postgresql/data

volumes:
    psql:
```
This now gave me persistant database access, as well as created a new db for me without having to run the `createdb` command from within the shell. Problem solved.

Before I get too far along with my project, I'm going to spend a little bit of time getting used to postgres. It's a very different beast.