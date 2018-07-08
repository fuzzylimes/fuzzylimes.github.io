---
layout: post
title:  "TIL: Getting Parameters to Express Routes"
date:   2018-07-07 21:15:00 -0000
categories: TIL
---
Today I spent most of my time working on a new side project. The project, titled [ute](https://github.com/fuzzylimes/ute) is a traffic generator template program to help quickly simulate REST traffic against a website.

The second part of this side project will be a management system for instances of `ute` running on various systems. The generator will probably sit in its current state for a bit while I'm able to get the management pannel working like I want.

Anyways, while working on this project today, I finally found an answer to a question I've had for just about as long as I've been working with express: how do I get varaibles to my routes in external route files?

Well, the answer is to use the `app.set()` command to set a parameter on the app (or whatever variable you used) associated with your express app. This value is actually accessible now through the `req.app` object over in the route!

And if you want to pass a value back to the main application? You can use `res.app.set()` to set a value and send it back to be accessible back in the main app.

I'm not sure why this never came up in any course or tutorial I did, seems like some pretty good knowladge to know...

💚