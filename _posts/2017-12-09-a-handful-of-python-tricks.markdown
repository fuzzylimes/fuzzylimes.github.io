---
layout: post
title:  "A Handful of Python Tricks"
date:   2017-12-09 21:10:00 -0500
categories: python
---
Different kind of entry today. Trying to keep things relaxed this morning. Working on another Twitch related scraping program that I'm just about done with. Here's a few things that I had to relean this morning.

### List of Dictionary Keys
Simply using `.keys()` on your dictionary will indeed return a list of the keys in the dictionary, but it's going to be a dict_keys object which you can't really do much with (aside from cycling through items in the list). In my case I wanted to reverse this list and start form the end first. To do so, you just simply need to mask it as a list:

{% highlight python %}
a = {}
a_list = list(a.keys())
{% endhighlight %}

### Reversing a List
This has always been one of those awesome "black magic" kind of tricks in python... and I use it so infrequently that I always forget about it. Using some neat splicing syntax, you can reverse a list without needing to make a copy of the original:

{% highlight python %}
a = [1,2,3,4,5]
b = a[::-1]
{% endhighlight %}

b will now equal `[5,4,3,2,1]`

### Creating a Folder If It Doesn't Exist
Another super handy thing that I always find myself needing... and forgetting. If you're going to be generating files to a folder, you'll want to make sure that the folder exists before you start writing the file:

{% highlight python %}
import os

if not os.path.exists(directory):
    os.makedirs(directory)
{% endhighlight %}