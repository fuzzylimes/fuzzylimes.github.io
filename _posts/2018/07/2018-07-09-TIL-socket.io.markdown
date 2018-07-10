---
layout: post
title:  "TIL: Learning Socket.io"
date:   2018-07-09 20:55:00 -0000
categories: TIL
---
Really starting to get out of my comfort zone today, and I love it.

I wanted to try to figure out a good way of doing live updates to the dashboard project that I'm working on, so I started doing a bit of googling around today on my lunch break. Thats when I found `socket.io`, a javascript package that handles websockets between your server and the client. It'll handle streaming data over from your server to your clients in real time, without having to refresh the browser (which is where I was heading to...).

This is a great exercise for two reasons.
1. It's making me lean this extreamly useful library
2. It's making me finally learn how to do DOM manipulation with javascript.

Once all of the data comes back from the server, I'll leave it up to the client to re-render the page in real time, as well as handle all of the calculations.

Still not really sure what the best way is to display all of this data, but I'll flush that out as I go along.

💚