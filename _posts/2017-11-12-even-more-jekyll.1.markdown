---
layout: post
title:  "Even More Jekyll"
date:   2017-11-12 20:25:00 -0500
categories: jekyll
---
I've been sick all weekend so I didn't have as much energy to spend on learning as I had wanted to. At the very least I was interested in seeing if I couldn't get the paging system to work, so I decided I'd spend what little remaining time I have this weekend playing around with it.

### Paging

All of the changes that I made to get paging working were based on the documentation on [jekyll's site](https://jekyllrb.com/docs/pagination/). The first thing that I noticed when looking at this page was that I made a small mistake when creating my seperate blog page. In order to break out my blogs, I had written a small `_includes` module called `latest.html`, which would handle the displaying of the blog posts. The idea being that I would use this on the main page to display a few of the records, as well as display it on the blogs page.

To handle the blogs page, I had create a new type of `_layouts` called `blog.html`. This was nealy identical to what was in the home page, so it really wasn't serving much of a purpose, but it did get me the seperate blog page I wanted.

Fast forward to this evening and reading about pages. In order for their pagination plugin to work, it expects the user to have an `index.html` file within a folder named the path you want it to show up at when viewing the page. This is along with the `blog.md` file in the root directory which directs to this path. Make sense?

Doesn't really make sense to me either, so I guess here's a picture of my directory structure to maybe clear it up:

![My helpful screenshot]({{ "/assets/img/2017-11-12.png" | absolute_url }}){:height="30%" width="30%"}



### Images
Nice little segway into images. Had to look up how to add assets to projects in order to get the snapshot above added in without the aid of imgur or some other hositng service. The solution was to create an `assets/img` folder, and then link to the file directly: `![My helpful screenshot]({{ "/assets/img/2017-11-12.png" | absolute_url }})`

The next issue was resizing. Evidently there are plugins you can install that will help you do it (already forgotten the name of the one that kept popping up), but I was able to find a solution for kramdown formatting ([see this page here, post on May15th from arganzheng](https://gist.github.com/uupaa/f77d2bcf4dc7a294d109)). All you need to do is add an extra thing of markdown to the end of your image, like so:

{% highlight markdown %}
![My helpful screenshot]({{ "/assets/img/2017-11-12.png" | absolute_url }}){:height="30%" width="30%"}
{% endhighlight %}

### Limiting number of items returned
I also wanted to set a limit on the number of blog entries that would be returned to the main page. This was as simple as adding a `limit` parameter to the for loop that sucks in the entries: 

{% highlight html %}
% for post in site.posts limit:5 %
{% endhighlight %}
This way I only get back the 5 most recent, and I'm ready to plug them into the home page (whenever that gets finished).


### Closing thoughts
I really thought I was going to hate jekyll, but the more that I play around with it the more I'm enjoying it. I'm looking forward to trying to making a nice looking landing page and about page this coming week (health permitting).