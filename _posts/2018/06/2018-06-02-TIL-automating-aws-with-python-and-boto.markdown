---
layout: post
title:  "TIL: Automating AWS with Python and Boto, pt1"
date:   2018-06-02 15:15:00 -0000
categories: TIL
---
I've been curious as to whether there was a way to automate the deployment/management of EC2 instances for a while now but only finally just got around to it today. Turns out there's a pretty nice package for Python that will handle a lot of it for you, called `boto`.

The package will allow for core things like querying for your active servers to get their status, starting up new instances of servers of n number and of y type, as well as pausing/stopping/terminating the servers. All pretty useful stuff, and the scripting for it seemed to be very straight forward.

It also seems to support the sending of commands to the instance. My original thought would have been to run the scripts needed to clone the test repo down to the box and get my services up and running... but the workflow doesn't seem right. There has to be a better way.

Still more research to do.

💚