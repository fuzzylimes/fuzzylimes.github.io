---
layout: post
title:  "Building Python Lists With Duplicate Records"
date:   2018-01-21 11:10:00 -0500
categories: python
---
This is one of those cases that really highlights how intuitive python is. I ran into a scenario where I needed to create a python list composed of multiple instances of the same value. Rather than building this list by hand I thought "surely there's a better way to be doing this...". Of course there was.

### My Scenario
For a work project, I'd previously created a program that would simulate some sort of device that would send data out to our DOT. Essentially I had written this using python's random() function to pick values from ranges that I had defined.

And all of that worked great when I was generating values where the parameter was a number. But what if the parameter needed to be from a specific list of values? And what if that specific list of values needed to be weighted to be more accurate to how the device would be sending these values.

So my first thought was to create a basic list, with each of the possible values in it:

{% highlight python %}
my_list = [0,1,2,3]
{% endhighlight %}

But this isn't what I needed. 90% of the time it should be 0, 5% of the time it should be 1, 3% of the time it should be 2, and 2% of the time it should be 3. So I needed to come up with way to get this list to get me these weighted values.

### My Solution
So the obvious place to start was with python's ability to multiply almost anything by anything. I'd used it with strings before, so I had a feeling I could use it with lists. So I tried it out:

```IN [1]: [1]*5 
OUT[1]: [1, 1, 1, 1, 1]```

Yes! That's what I was looking for. But now if only I could get all of my numbers added all at once. Maybe try something like adding them?

{% highlight python %}
my_list = [0]*90 + [1]*5 + [2]*3 + [3]*2
{% endhighlight %}

Bingo! Now all I needed to do was add in the logic to select from it:

{% highlight python %}
import random
return random.choice([0]*90 + [1]*5 + [2]*3 + [3]*2)
{% endhighlight %}

Sometimes the most obvious solution gets the job done.