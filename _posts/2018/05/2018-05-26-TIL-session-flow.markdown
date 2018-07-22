---
layout: post
title:  "TIL: Session Flow"
date:   2018-05-26 21:25:00 -0000
categories:
  - Coding
tags:
  - node.js
---
Today marks 28 days in a row of TIL posts. When I started out a month ago, I knew that I wanted to spend a little bit of time each week reflecting on what I'd been doing, and I figured that a blog post would be a great way to capture that. I never expected that I'd be able to keep it up for as long as I have, let alone an entire month. So that's a pretty crazy accomplishment, one that I'm super proud about.

One thing that the past month has really tought me is that you actually learn a lot on a daily basis. So much so that it's hard to figure out what to actually write about at the end of the day. A lot of what I learn has nothing to do with the scope of this blog, which tends to make my evening entries a little bit tricky. While I've deviated some in the past, I really do want to keep thigns more focused on tech/coding things that I learned. It really can be something as simple as a cleaner way of approaching something.

Four weeks straight. Pretty crazy.

## Session Flow
While today was a pretty relaxed day (ended up working for 4-5 hours on my work project), I did take some time to start reading into handling sessions within my express app I'm working on. Unlike the previous websites that I've made, the one that I'm working on for work really needs to have some type of stateful sessions saved somewhere.

So todays reading took me down the path of how I can somehow store sessions within my application. This led me into looking into the `express-session` module. It simplifies some of the common session handling tasks for you, like generating and handling your cookies. I haven't had a chance to play around with it yet, but it seems simple enough.

With what I was able to read through today, I have a basic idea of what I need to implement within my application to maintain a record of users, their credentials needed to interact with the server, and handle the expiration of those credentials.

Next steps are going to be playing with this module and trying to figure out a simple way of managing these sessions without a database (app runs local on users system, database is overkill). But that's for tomorrow.

💚