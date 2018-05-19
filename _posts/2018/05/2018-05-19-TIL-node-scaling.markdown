---
layout: post
title:  "TIL: Intro to Scaling Node Apps"
date:   2018-05-19 16:45:00 -0000
categories: TIL
---
Struggling through some food poisoning today, so I don't have much to talk about. Before things got too bad, I did do some reading up on how to scale out nodejs applications. My intention for this weekend was to convert one of my python apps for work over to using nodejs and then scale it out, but this illness kind of put a damper on that.

In the meantime I wanted to start getting an idea of how node actually scales out. One thing that I wasn't aware of before today is that nodejs instances are all single threaded. The async nature is handled amongst that single thread. This makes scaling easy as you just need to run more instances on more cores. And node happens to provide a way to communicate between all of those instances.

Because I'm not really feeling up to doing a review, I'll just leave the [link to this very helpful article](https://medium.freecodecamp.org/scaling-node-js-applications-8492bd8afadc) that goes into detail about the whole process.

Hope to play around with this tomorrow, but for now it's rest.

💚