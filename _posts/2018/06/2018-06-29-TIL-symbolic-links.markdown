---
layout: post
title:  "TIL: Using Symbolic Links with Node"
date:   2018-06-29 22:15:00 -0000
categories:
  - Coding
tags:
  - node.js
---
Today I had a request to make some of my log files accessible via the server that I was running. Log files for my test application are getting written in one place, so I needed some way to get them to the public folder in express where they would be accessible. In order to do this, I created symbolic links to the log files within the public folder.

I'd run into linked files in the past, but this was actually my first time creating them myself. In order to link the files, all you need to do is run the `ln -s <path/to/file> <path/to/link>` command. This will create a symbolic link back to the file, making it accssible via this new folder. In my case, I was able to make these files selectively accessible from the outside assuming you knew the folder.

💚