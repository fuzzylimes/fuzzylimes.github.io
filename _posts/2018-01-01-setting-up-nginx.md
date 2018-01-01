---
layout: post
title:  "Setting up nginx"
date:   2018-01-01 15:10:00 -0500
categories: nginx
---
As I mentioned in my last post, I'd fummpled my way through nginx when trying to get my first website deployed. Well, today I tried to get my second site deployed and hit another set of issues, so I figured now was as good a time as any to make a blog post about it.

## The Problem
Originally I needed to use nginx as a reverse proxy for one of my sites. I had followed through the tutorial [on this site](https://code.lengstorf.com/deploy-nodejs-ssl-digitalocean/) to get it working for one of my domains, but today I wanted to set it up for a second. Since my site has such low traffic, I wanted to run both of my sites on the same box. So some changes needed to be made, but I wasn't really sure what exactly.

So this blog post is going to cover how I was able to get this running, and the changes I had to make to my files to do so.

## The Solution
This is going to be more of a thought dump than a full on tutorial.

### Getting the base files ready
I like to do prep work before I get started. In order to use nginx, you need to create .config files that it pulls from. The basic structure of these files looks something like this:

{% highlight bash %}
# HTTP — redirect all traffic to HTTPS
server {
    listen 80;
    listen [::]:80;
    server_name domain1.com www.domain1.com
    return 301 https://$host$request_uri;
}

# HTTPS — proxy all requests to the Node app
server {
    # Enable HTTP/2
    listen 443 ssl http2;
    listen [::]:443 ssl http2;
    server_name domain1.com www.domain1.com;

    # Use the Let’s Encrypt certificates
    ssl_certificate /etc/letsencrypt/live/domain1.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/domain1.com/privkey.pem;

    # Include the SSL configuration from cipherli.st
    include snippets/ssl-params.conf;

    location / {
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-NginX-Proxy true;
        proxy_pass http://localhost:8000/;
        proxy_ssl_session_reuse off;
        proxy_set_header Host $http_host;
        proxy_cache_bypass $http_upgrade;
        proxy_redirect off;
    }
}
{% endhighlight %}

In this example, I have two different server blocks. The reason for this is because I'm using https. The first block handles the re-routing from http to https. The second block is where all of the logic goes for the domain.

In both blocks you'll notice a `server_name` parameter. This is a space separated list of all of the domains and subdomains that should be using this specific app (you'll be creating one of these sets for each of your files).

In the second block, the encription files that were generated during the tutorial get pulled in, including the generated SSL cert.

Finally comes the location. The blob is pretty much boiler plate. Note in this example that the location is set to the root path (`/`). This is where the link between your running app to your domain is created. This is the magic glue that took me 3 days to understand and stop being lost. The `proxy_pass` line needs to be changed to point to the port where your application is running.

### Creating the files
Using that template from up above, we'll need to go ahead and make a `.config` file for each of the domains that we want to use on the server.

These `.config` files will all be stored in the `/etc/nginx/sites-available/` folder. Create a new file for you specific domain, such as `sudo vim /etc/nginx/sites-available/domain1.com`. Dump the snippet from the previous section into this file, updating the `server_name` and `proxy_pass` lines as needed to match your application.

Repeat this process for every domain you want to use on the server.

### Updating the nginx.conf file
In order to avoid having to do a symbolic link between the files we just created in the `/etc/nginx/sites-available/` folder to files of the same name in `/etc/nginx/sites-enabled/`, it's much easier just to update the `nginx.conf` to use this directory instead.

Run `sudo vim /etc/nginx/nginx.conf` and change the following:

{% highlight bash %}
include /etc/nginx/sites-enabled/*;
{% endhighlight %}

to

{% highlight bash %}
include /etc/nginx/sites-available/*.conf;
{% endhighlight %}

This will cause nginx to pick up your newly created config files when it starts up.

### Restart nginx
After making these changes, you'll need to restart nginx for the changes to take effect. In my case, using `sudo /usr/sbin/service nginx restart` was not working for me and my changes were not taking effect. To actually get the changes picked up, I had to do a `sudo /usr/sbin/service nginx stop` and `sudo /usr/sbin/service nginx start`