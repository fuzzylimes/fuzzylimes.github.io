---
layout: post
title:  "TIL: Folders in Jeykl and Docker Images"
date:   2018-03-31 17:00:00 -0500
categories: TIL
---
Today was lowkey, busy with a lot of house work, but I did manage to find a few new things to work on. The first was with my continued learning of Docker and learning about images. The second was a organization activity for Jekyll.

## Docker Images
Almost all of the info I'm about to dump here is available on ['This github gist'](https://gist.github.com/fuzzylimes/0247cc03e5b7f84b6eb58231ba827179).

The lessons I worked on today were all about images. So covering everything from what an image really is, to building your own and getting it uploaded onto DockerHub.

### What are Images?
Docker images consist of different layers that together defined a specific environment. Layers consist of anything from OS type files (your base ubuntu, alpine, etc), package commands (`apt`, `yum`, etc), environment variables, shell commands, system changes, etc. Each of this actions, which get defined in your Dockerfile, are a layer.

Each of these layers are then hashed so that Docker can do a certain level of caching to reduce build time. If a certain line in a Dockerfile changes, only the changed layer and below will need to be redone. This makes docker extremely performant.

### Image tagging
* Tags are pointers to specific image commits
* `docker image tag nginx fuzzylimes/nginx` - tag existing image with a new tag
* `docker image tag fuzzylimes/nginx fuzzylimes/nginx:testing` - tag same image with a different (specific) tag name
* `latest` tag is default. Used to represent the most recent and stable version

### Uploading image to Docker Hub
* `docker login` - Login to DockerHub
* `cat .docker/config.json` - view file
* `docker logout` - Delete login key
* `docker image push fuzzylimes/nginx:testing` - push image file to Docker Hub
* If using a private repo, create repo first before pushing

### Dockerfile
* `docker image build -t customnginx .` - build image from dockerfile with tag in the specified directory
* `FROM` - Defines the image to be used as the base
* `RUN` - Runs a command (bash) inside the container
* `WORKDIR` - Correct way of setting the working directory in a container (i.e. same as `cd`ing to path)
* `COPY` - Copy file into WORKDIR path

### Asignement
The final assignment I had to do was to create a Dockerfile that would spin up a node program, which was accomplished with the following below:

``` Dockerfile
# Instructions from the app developer
# - you should use the 'node' official image, with the alpine 6.x branch
FROM node:6-alpine
# - this app listens on port 3000, but the container should launch on port 80
  #  so it will respond to http://localhost:80 on your computer
EXPOSE 3000
# - then it should use alpine package manager to install tini: 'apk add --update tini'
RUN apk add --update tini \
# - then it should create directory /usr/src/app for app files with 'mkdir -p /usr/src/app'
    && mkdir -p /usr/src/app
WORKDIR /usr/src/app
# - Node uses a "package manager", so it needs to copy in package.json file
COPY package.json package.json
# - then it needs to run 'npm install' to install dependencies from that file
RUN npm install \
# - to keep it clean and small, run 'npm cache clean --force' after above
    && npm cache clean --force
# - then it needs to copy in all files from current directory
COPY . .
# - then it needs to start container with command '/sbin/tini -- node ./bin/www'
CMD ["/sbin/tini", "--", "node", "./bin/www"]
# - in the end you should be using FROM, RUN, WORKDIR, COPY, EXPOSE, and CMD commands
```

## Jekyll Folders
Maybe it's just so obvious that it's not written down, but I never got the memo that you could actually organize all of your blog posts in folders within the `_posts` folder. I assumed that if you created folders that it would blow up all of your existing logic and nothing would work anymore.

Turns out you can totally make folders to organize your posts and Jekyll will just ignore them all. Not sure why this isn't explicity stated somewhere.

So before today, I had every one of my blog posts all at the same level in the same folder. Almost impossible to find the file that I may have wanted, and not see the ones that I didn't.

Now everything is broken down by year and month sub folders, making it 100x more enjoyable to work with:

![User section]({{ "/assets/img/2018-03-31.png" | absolute_url }})