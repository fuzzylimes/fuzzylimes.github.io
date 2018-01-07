---
layout: post
title:  "Bundling Python Packages"
date:   2018-01-07 14:30:00 -0500
categories: python
---
Making good on one of my new years resolution, I took the time to learn how to bundle Python projects up into nice little distributable packages. Figured I'd write down what I leaned for future me.

For whatever reason, I always thought the process of bundling projects was complicated and never bothered looking into it. I assumed the ammount of time it would take to read up on it would be more than what I'd get out of it. After all, I could just import my projects from their folders as I needed them.

Boy that was dumb.

As outlined in this [super easy to follow guide](http://python-packaging.readthedocs.io/en/latest/minimal.html), there's absolutely nothing to be affraid of.

I followed this guide up until the point that they were having you create an account and get your modules into the pypi repo. I was less interested in doing that, and more interested in allowing for installs straight from github.

The guide does a good job of explaining what basic folder structure needs to be, so I'm not going to bother repeating it here. The one non-obvious 'gotcha' that I hit was with creating the `__init__.py` file. I knew that they were used to make something useable within a package, but I never had put anything in them. I found that when trying to import your module, that you have to prefix it with a `.` to denote that the file is in your current folder. This was actually in the example, but I glossed right over it.

So that brings me to the installation portion that I was most interested in. If you've commited your package to github with a setup.py file in it, you have one of two options: you can either clone the repo and install using setup.py, or you can install directly from github. That's what I was interested in.

To do so, you'd run something like the following:
`pip install git+git://github.com/fuzzylimes/mal-scraper.git`
Where the URL is pointed to the package you want to install. Again, note that this will only work if there is a setup.py file present in the repo you're trying to install.

What's super neat about this is that all of your dependecies will be installed automatically for you.