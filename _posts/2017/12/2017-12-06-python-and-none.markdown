---
layout: post
title:  "Python and NoneType: My Constant Battle"
date:   2017-12-06 21:10:00 -0500
categories:
  - Coding
tags:
  - python
---
As I mentioned before, one of my goals of this blog was to try and get more of the common issues I run into to finally stick. There are some things that I have to look up again, and again, and again, well beyond the point where it would have been benifitial to just learn the damn thing. So today's post is going to look at one of those things: python and NoneType.

I'm not sure why this always causes me so many issues, but it does. Any and every time I want to check to see if a value is None, I always want to do this:

{% highlight python %}
a = None
if a == None:
    return "I'm None!"
{% endhighlight %}

Always. Every. Single. Time.

I know I've googled it. Every single stack overload thread on the first page has been visted, more than once! Then, inevitably, the next thing I jump to is trying to remember what that one command is for checking the type of an object... oh yeah, `isinstance`! So then I jump into the next mistake:

{% highlight python %}
a = None
if isinstance(a, None):
    return "I'm None!"
{% endhighlight %}

Surprise, None is not a type! Okay, maybe it has to be NoneType:

{% highlight python %}
a = None
if isinstance(a, NoneType):
    return "I'm None!"
{% endhighlight %}

...NoneType is unknown. Great.

## The Solution
The reality is that there are a few ways of actually doing this verification.

### 1. Use 'is'
This is kind of the exception to the rule, but also requires the least amount of key strokes. Revisitng the previous examples:

{% highlight python %}
a = None
if a is None:
    return "I'm None!"
{% endhighlight %}

Simple and straight to the point

### 2. Use "type()"
Using type() to check the type of the variable, as well as None, allows you to do the comparison a few different ways. The example from before can be updated like so:

{% highlight python %}
a = None
if isinstance(a, type(None)):
    return "I'm None!"
{% endhighlight %}

Also you could use type on the variable and do a simple direct comparison:

{% highlight python %}
a = None
if type(a) == type(None):
    return "I'm None!"
{% endhighlight %}

Maybe I'll remember next time I need to check for None... Probably not.