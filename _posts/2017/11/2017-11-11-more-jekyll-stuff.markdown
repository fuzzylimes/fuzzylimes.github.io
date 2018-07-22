---
layout: post
title:  "More Jekyll stuff"
date:   2017-11-11 09:47:00 -0500
categories:
  - Coding
tags:
  - jekyll
---
Spent some more time this morning trying to figure out Jekyll. I'm not sure why they try so hard to hide the functionality from the user. Maybe I'm just bad at reading the documentation...

Here are a few things I wish I had known up front before getting started with everyting:

### Themes define your site
Yesterday I was trying to figure out where the html/css files were for the page and how I could make changes to them. It wasn't until this morning when I sumbled across [this page](https://jekyllrb.com/docs/themes/#overriding-theme-defaults) when I confirmed my suspicion that the themes control your site.

And that makes perfect sense, I just wish that was mentioned form the get go. Maybe "theme" is a common term for people coming from previous webblogging platforms (perhaps wordpress?), but it was non-obvious to me.

Anyways, themes are basically templates that allow you to define chunks of your site, sucking in the stuff that you care about. All of these are defined within the theme files. You can find where those theme files are located on your computer by running `open $(bundle show <theme>`. This will take you to the directory where all of the template files for this theme are located.

If you want to make a change to the theme (I'm still using the default `minima` at the time of writing), you would create the corresponding folders/files within your project. The folders to look at would be the `_layouts`, `_includes`, and `_sass` folders. Then you'd simply make a copy of what needs to be changed (i.e. `_layouts/page.html`) and make your updates. This will then override the default theme settings. The same applies for `_includes` and `_sass`.

### Handling multiple posts on the same day
In the case that you decide to make more than one post on the same day, you need to add an extra yaml parameter to the top of your posts to ensure that the latest is displayed first.

In my case this parameter was already present in my default post during generation: `date`. This parameter defines not only the date, but also the time of the post, which will allow more rescent posts to appear in the top of the list.

Sample date for this post:
{% highlight yaml %}
layout: post
title:  "More Jekyll stuff"
date:   2017-11-11 09:47:00 -0500
categories: random
{% endhighlight %}

### Other useful resources
* [Setting time stamps in jekyll](https://learn.cloudcannon.com/jekyll/date-formatting/)
* [Jekyll markdown cheatsheet](https://gist.github.com/roachhd/779fa77e9b90fe945b0c)
* [Jekyll markdown - kramdown site](https://kramdown.gettalong.org/index.html)

## Where to next?
1. ~~I'd like to break out the blogs so that they're on their own page and repurose the home page into more of a home page.~~
2. Enable paging for the posts page.
3. Create a tollerable home page.

