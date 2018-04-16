---
layout: post
title:  "TIL: docker-compose"
date:   2018-04-15 16:00:00 -0000
categories: TIL
---
Finally found some time to work through another section of the Docker course I'm taking. Today was all about `docker-compose.yml` files and using the docker-compose application for quick deployments. It makes standing things up super quick with just a few configuration files.

## The `docker-compose.yml` file
We can use this file to define how we want an evironment to be build. Basically this is used to abstract all of the `docker container run` commands which can start to get out of control. The compose file can be used to set up not only your instances, but also the volumes and networks you want created. This is saved into a file making it super easy to spin the same exact thing up every time.

The files themselves are pretty straight forward. It's a simple yml file that's very intuitive to read. Here are a few examples

#### Example 1 
```yaml
version: '2'

# same as
# docker run -p 80:4000 -v $(pwd):/site bretfisher/jekyll-serve

services:
    jekyll:
        image: bretfisher/jekyll-serve
        volumes:
            - .:/site
        ports:
            - '80:4000'
```

#### Example 2
```yaml
version: '2'

services:
    
    wordpress:
        image: wordpress
        ports:
            - 8080:80
        environment:
            WORDPRESS_DB_PASSWORD: example
        volumes:
            - ./wordpress-data:/var/www/html

    mysql:
        image: mariadb
        environment:
            MYSQL_ROOT_PASSWORD: example
        volumes:
            - ./mysql-data:/var/lib/mysql
```

## Using the docker-compose CLI
Once you've got your `docker-compose.yml` file created (or some other yml file, you can use a `-f` flag when running), you can then spin up the contents of that file using the `docker-compose` command. Note that in the case of linux installs, `docker-compose` needs to be installed seperately from the base docker install. See installation docs online for it. Windows and Mac are supposed to come with it.

The commands are pretty stragiht forwards here:
* `docker-compose up` - streaming logs
* `docker-compose up -d` - run in background
* `docker-compose logs` - get logs from compose (same as those streamed)
* `docker-compose ps` - list containers run by docker-compose
* `docker-compose down` - stop and cleanup

## Dealing with named volumes
In order to use named volumes, an additional parameter has to be added to the `docker-compose.yml` file at the bottom for `volumes`. In the example below, we're creating 4 names volumes that will persist after the services are brought down:

```yaml
version: '2'

services:
    drupal:
        image: drupal
        ports:
            - '8080:80'
        volumes:
            - drupal-modules:/var/www/html/modules
            - drupal-profiles:/var/www/html/profiles
            - drupal-themes:/var/www/html/themes
            - drupal-sites:/var/www/html/sites
    postgres:
        image: postgres
        environment:
            POSTGRES_PASSWORD: example
volumes:
    drupal-modules:
    drupal-profiles:
    drupal-themes:
    drupal-sites:
```

In order to cleanup these volumes that are created, you can run the `docker-compose down -v` option and the volumes will be destroyed when the services are stopped.

Another note that the `--help` command is your friend when looking at what `docker-compose` can do.

## Handling builds
You can combine a `Dockerfile` along with a `docker-compose.yml` file to build your own image. In order to do this, you just need to add a `build` parameter to your service listing in the `docker-compose.yml` file. This will point to the location of the Dockerfile to use for building.

Here's a small example of linking the two:
#### docker-compose.yml
```yaml
version: '2'

services:
    drupal:
        image: custom-drupal
        build: .
        ports:
            - '8080:80'
        volumes:
            - drupal-modules:/var/www/html/modules
            - drupal-profiles:/var/www/html/profiles
            - drupal-themes:/var/www/html/themes
            - drupal-sites:/var/www/html/sites
    postgres:
        image: postgres
        environment:
            POSTGRES_PASSWORD: 
        volumes:
            - drupal-data:/var/lib/postgresql/data
volumes:
    drupal-modules:
    drupal-profiles:
    drupal-themes:
    drupal-sites:
    drupal-data:
```

#### Dockerfile
```Dockerfile
FROM drupal:8.2

RUN apt-get update && apt-get install -y git \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /var/www/html/themes

RUN git clone --branch 8.x-3.x --single-branch --depth 1 https://git.drupal.org/project/bootstrap.git \
    && chown -R www-data:www-data bootstrap

WORKDIR /var/www/html
```