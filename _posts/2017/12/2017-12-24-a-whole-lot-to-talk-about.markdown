---
layout: post
title:  "A Whole Lot to Talk About"
date:   2017-12-24 21:00:00 -0500
categories:
  - Coding
tags:
  - node.js
---
So, it's been a while. Where do I even begin...

## My First Website Deployed
So a while back I talked about a little program I was working on to srape games played on twitch streams. That was a fun project that I left open source and continued to put a bunch of differnt utilities into. I think it's at a point now where the only thing that really needs to be touched up is the documentation.

One of the utilities that went into that was the static web page generation that I showed off in the last post. After giving it a lot of thought I decided to take a step out of my comfort zone and actually build a web site that would display all of this information, rather than just having the static files.

The first thought was to make a simple server that would serve up the static html files that were being generated. But as I started to plan and code that out, I wasn't really feeling it. The whole static file generation seemed silly. There had to be a better way.

So I decided to go ahead and write a tool that would enable all of the data to be crunched and then saved to a mongodb. This mongodb could then be used to pull data needed to display the pages as needed. Seemed easy enough, but also something that I really didn't know what I was doing.

My basic gameplan was something like this:
* Use node.js + express to handle the server
* Use the handlebars templating engine to create the webpages
* Deploy the server? Or something
* Hook up domain and add tracking?

From that list, I had briefly done the first 2 items in a tutorial that I never really finished (but that's a story for another time).

### Setting up the server
I've had experience with two different server technologies over the last few months: flask and nodejs. Since I've previously created projects at work using flask to make APIs, I decided that node.js would be a better thing to try. I'd done some MEAN stack stuff (unsuccessfully) in the past, so at least I was familiar-ish with how things worked.

So using express, I went ahead and started planning out how the site would work. Imediately I ran into an issue with how to handle routes for pages you don't know will exist. For example, If I want to have a `example.com/fruits/apples` and `example.com/fruits/banana` page on my page, there had to be an easier way to do it than creating static routes AND to acccount for multiple fruits.

Looking around the internet, I wasn't able to find anything that really explained what I was trying to do... which I'm not sure if that's because the problem is so obvious or if I wasn't searching for the right thing. But, after spending some time playing around with it, I was able to get something working just like I wanted. Using the example from before, this would look something like `example.com/fruits/:fruit`. This then allows the variable (`fruit` in this case) into the path function.

Speaking of functions, during all of this I struggled through learning how to work with ascyncronus functions. This sort of broke my mind, trying to understand how to handle callbacks and actually get thigns to run in the order that I needed them to (another topic for another day).

### Using Handlebars
In order to get the page rendered for all of the dynamic pages that I'd be using, I chose to use handlebars. Since it's more or less enhanced html, it was easy to get all of the items I'd already been using in my html generator ported over into their handlebars counterparts. This was pretty straightforward for the most part...

... until I got to the point where I needed to try to run a function on data I was passing into the template. In my case, I wanted to change the dates that were coming out of the database. Again searching wasn't going to well, until I stubled upon one response that made note of a concept called `helpers`. This meant that a function could be created and then used during the replacement. I'll give an examples:

Inside my app, I created a `helpers.js` file that created and exported functions so that the whole program had access to them:

{% highlight javascript %}
module.exports = {
    fixdate: function(dateString){
        return dateString.replace(/\:/g, "-");
    },
    formatdate: function(dateString){
        let monthNames = ["January", "February", "March", "April", "May", "June",
            "July", "August", "September", "October", "November", "December"
        ];
        let temp = dateString.split('-');
        return monthNames[temp[1]-1] + " " + temp[0];
    },
    formatstreamdate: function(dateString){
        let temp = dateString.split('T');
        return temp[0] + " (" + temp[1].slice(0,-4) + " UTC)";
    }
}
{% endhighlight %}

So then, if I wanted to use one of these functions in the handlebars script, I could simply do:

{% highlight html %}
{% raw %}
<div class="container mt-4">
    <div class="row justify-content-center">
        <div class="h3">History for {{formatdate history}}</div>
    </div>
</div>
{% endraw %}
{% endhighlight %}

One other small "gotcha" I ran into was trying to access other variables from within an `#each item` loop. With the way that handlebars works, once you enter the each loop, the focus is on the object you're itrating through. If you want to pull in a different variable, you'd need to actually go up another level to access it, like so:

{% highlight html %}
{% raw %}
<div class="container history-links">
    {{#each months}}
    <h3><a href="/streams/{{../user.lower_name}}/history/{{this}}">{{formatdate this}}</a></h3>
    {{/each}}
</div>
{% endraw %}
{% endhighlight %}

### Deploying
This was the most daunting part for me. I wasn't really sure where to start, what service to use, what fees to worry about, etc etc. Eventually I landed on the following:

* Host website on a Vultr EC2 instance
* Host mongodb on mlabs

This would keep my monthly bill low at around $5 a month, and have plently of room for future projects, as well as running the scraping program.

Great! But now what? Thankfully I found [this tutorial](https://code.lengstorf.com/deploy-nodejs-ssl-digitalocean/) that walk through the whole process of getting your app deployed and setting up various security items (including SSL!). However, I had read some stuff saying not to use the `PM2` package to monitor your app status and to use `systemd` instead. For that, I was able to fumble my way through it using some items I found online, including this [stack overflow post](https://stackoverflow.com/questions/36417528/how-to-auto-restart-node-app). This post is already way too long, so that'll have to be saved for another post.

### Connecting Domain
This I had to figure out on my own. Every tutorial I could find online were for different registries than where I purchased my domain through... so I poked until I got it working. To my surprise, it really is as simple as editing your DNS records for your site, giving it a path (subdomain in my case), and then pointing it at a server. That's it. It just works.

## The Site
So, after two weeks of working and not sleeping, here's where my project currently stands: [https://stats.fuzzylimes.com/](https://stats.fuzzylimes.com/).

Looking forward to making more improvements to it in the future.