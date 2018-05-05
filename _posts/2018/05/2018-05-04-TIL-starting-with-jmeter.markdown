---
layout: post
title:  "TIL: Starting with JMeter"
date:   2018-05-04 21:15:00 -0000
categories: TIL
---
So today I took a little detour from my normal every day work to play around with learning JMeter. We're reaching the home stretch on our project and we really need to start getting the performance testing rolling in our group. Development has already done some of that testing, but we need to have some of our own running.

So I'd heard about JMeter a few years back, but honestly didn't really know anything about other than it was used to do load testing. I was under the impression that it was a javascript app that was installed via node and that you wrote javascript code to drive the tests.

Turns out that wasn't right at all. JMeter is a Java program, and it requires either the JDK or JRE to be installed to use. It has everything and the kitchen sink included. Forget being limited to only writing load/performance testing, you could write your entire test set using it.

Most of my time today was spent watching videos and trying to learn how to write my own functions and handle variables. From what I could find, functions can easily be written in one of the supported languages within a pre-condition item, store a value into a variable, and then suck that variable into the messages you're sending.

Still very new to the tool but I'm actually pretty impressed with what I played around with today. It seems like it alows for a lot of flexibility and freedom to do things the way that you want to. And the fact that you can just add in any new java libraries that you want to is a huge plus.

I'm sure there will be more blog posts to come once I get more hands on time with it.

💚