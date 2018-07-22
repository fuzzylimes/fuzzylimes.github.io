---
layout: post
title:  "Python virtualenv weirdness"
date:   2017-11-26 21:52:00 -0500
categories:
  - Coding
tags:
  - python
---
After getting pissed off again trying to work my way through front end (Angular 4...) training the last two days, I finally reached my breaking point and rage quit. Not having any fun, need to take a break and do something that's actually interesting/enjoyable for me. So I decided that I'd go ahead and work on one of the Python courses I'd also previously picked up. All was well until I hit a point where 1: I needed to install the cv3 image processing; and 2: using global packages with virtualenv.

## Setting up CV3 for mac
The first issue was a mac specific issue. Probably the first time where the installation was actually more difficult for mac than it was for Windows. The instructions provided in the lesson were old/out of date and suggested using python2 for the rest of everything as the python3 version wasn't ready. Googling around showed that CV3 for python3 has been ready for a while and working. Which then brought me to the point of trying to install it.

I came across [this posting here](https://www.learnopencv.com/install-opencv3-on-macos/) for how to get it installed. In my case I was able to skip almost everything on this page and simply run step 5.1. In doing so, brew installed the following packages for me:
>sqlite, gdbm, python3, python, eigen, lame, x264, xvid, ffmpeg, jpeg, libpng, libtiff, ilmbase, openexr, numpy, tbb

With that I was then able to access cv3 globally by starting python3 and importing cv2 (why is this 2? I don't understand yet....).

## venv weirdness
So my next goal was to be able to create virtual environments that would be able to use this global value. Some googling led me to find the `--system-site-packages` parameter when creating a new virtual environment. Great! This should solve all my problems!

But no, this only seemed to create a new problem. When generating the virtualenvironment using `python3 -m venv numpy --system-site-packages`, sourcing in, and then pip installing my packages, I found that the installed packages were not accessible (`ipython` and `jupyter` in my case). Trying to launch either would spit out errors about the files not existing. Bummer.

Then I noticed that this was not the command that I was used to running when generating virtual environments. So I tried the `virtualenv -p python3 numpy --system-site-packages` method that I'm used to using, and success! All of my packages are loading now and I've got access to the global (cv2) that I need. Why does this work? Dunno. Too late to look into it now.

## Bonus
Because I cannot ever remember this, maybe posting it will help it stick. To check to the full size of a folder and all of its contents on linux/unix, use: `du -sh <file_path>`. That will give you the size of the folder and all contents.