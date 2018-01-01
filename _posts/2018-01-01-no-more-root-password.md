---
layout: post
title:  "Don't require password for nginx start/stop/restart/status"
date:   2018-01-01 15:25:00 -0500
categories: nginx
---
It's the start of a new month, which means that one of the helper scripts for my new site finally ran! ...and it failed terribly and brought down my server for ~5 hours.

## The problem
When setting up my site last month, one of the steps that was taken was to configure a cron job that would stop nginx, try to refresh my ssl certificate, and then start nginx back up. Well, I had enough permissions to stop the service, but it never got started back up agian.

In order to avoid this, I wanted to find a way to allow permission for my user to run the ngnix commands without having to use the root password.

## The solution
After much googling and many different tries, I landed on [this solution](https://gist.github.com/sheharyarn/f3d98e8cc859f092532b).

In my case I decided to not map the commands to an alias and just set the permissions for the commands specifically. Create a new sudoers record by running `sudo visudo -f /etc/sudoers.d/username` and adding the following:

{ % raw % }
username ALL=(ALL) NOPASSWD: /usr/bin/service nginx start,/usr/sbin/service nginx stop,/usr/sbin/service nginx restart,/usr/sbin/service nginx status,/opt/letsencrypt/letsencrypt-auto renew
{ % endraw % }

> Note: change username in the previous example to the user that will be running the command.

Using this method, you will HAVE to spell out the full path when running the command. `service nginx status` will NOT work. It must be `/usr/bin/service nginx status`.

Looking back at it, the solution in that gist link is much better than the way that I implmented it. Just use that one.