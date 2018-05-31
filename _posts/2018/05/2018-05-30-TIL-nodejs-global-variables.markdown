---
layout: post
title:  "TIL: Global Variables"
date:   2018-05-30 21:35:00 -0000
categories: TIL
---
Still working though sessions. The tutorial didn't turn out to be everything that I wanted it to be, but I think I may have found a way around it. Just haven't had time to explore enough to have my answer on whether or not it's going to work. In the mean time, I learned how to set a global variable today, despite the internet yelling at me not to.

All you need to do is prefix your variable with `global` and it'll be accessible from your other files. So in my case, after breaking out my routes into sepearte route files, I needed to access some of the variables defined in my main file. By changing them to `global.variable`, they can then be used by their name (i.e. `variable`) in other files.

💚