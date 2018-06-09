---
layout: post
title:  "TIL: Reordering Window numbers in screen"
date:   2018-06-08 21:30:00 -0000
categories: TIL
---
I've been a big user of the `screen` application for years now. It's super handy when working on cloud instances as it seems to always be there as part of the base install, keeps your work space organized, and can keep you from opening up 30 ssh terminals.

I know that there are a bunch of different applications that are "better" than `screen`, but the ones that I tried were always too complex and I could never remember how to swap my screens and such. `screen` is simple enough to get me up and running with next to 0 effort.

One thing that I'd always wanted to know was how to reorder the windows that I create. I always like to order things for my work flow, but maybe I get one window session running in an area that doesn't fit that work flow.

Well, turns out it's pretty simple to change. [From this post here](https://serverfault.com/a/282279), it's as simple as:
1. navigate to the window that you want to move
2. `ctrl+a :number <window number>`

If another window already exists at the number you're moving to, the two will be swapped out. So in the example of `ctrl+a :number 3`, the current window will be moved to 3, and the window at 3 will be swapped with your current window number.

💚