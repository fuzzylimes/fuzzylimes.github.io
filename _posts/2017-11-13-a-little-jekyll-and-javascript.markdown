---
layout: post
title:  "A little jekyll and Javascript"
date:   2017-11-13 21:12:00 -0500
categories: jekyll, javascript
---
Sick again and busy with work, but I still wanted to take a few minutes to write about what I did learn today. Not a whole not to report on today, just a few things come to mind with regards to jekyll and some Javascript stuff that I did for work.

### More playing with jekyll layout
Of the three main goals I had for expanding this little blog page, the last one remaining was getting a pretty landing page set up. My goal was to take some of the work I'd done before in side projects from some of the youtube videos I'd watched, and throw together something nice.

Aside from the fact that I will never find work as a front end developer, I did learn a little bit more about how the default jekyll template is setup. The header that generates the navbar will dynamically scan your site for pages and add them for you automatically. I'd known something was happening before when I added the break out blog page, but it became more apparent when I created a new standalone landing page. Like with the blogs, I created a new page folder and dropped the `index.html` page inside and voila, all taken care of.

The landing page is no where near ready to be added in yet, maybe this weekend if I find the time.

### Little bit of JS
The tool we currently use to test with at work allows for some custom JS to be plugged in. Coming from python, enough of it seems to carry over that the way I approach a problem is more or less the same, but the syntax always throws me off.

In todays case I wanted to take a comma separated string, split on the commas to give me an array of strings, slice that array to ignore the first value, then finally split this list into two lists.

Spliting was easy enough. Simply use the `.split()` array method with whatever character you want. Done.

Next was the slicing. With python, I'm used to doing something like `list[1:-1]` to grab the second through final item. I quickly found that -1 in JS was NOT the last item in the array, but rather the second to last. So instead of setting a begining and an end, simply setting the start was enough: `array.slice(1)`.

Finally it was time to split that array in half. Again, I wanted to use some sort of slicing, but instead found something new to me called splicing. Similar to slicing, only whatever is contained in the slice will be removed and assigned to a new variable. So in my case I did something like this:
{% highlight js %}
var list2 = ['a','b','c','d','e','f','g'];
var list1 = list2.splice(0,Math.ceil(list2.length/2));
{% endhighlight %}
This gives a `list1` value of `['a','b','c','d']` and a `list2` value of `['e','f','g']`. Then I could join my list back into strings as needed.