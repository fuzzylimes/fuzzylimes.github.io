---
layout: post
title:  "TIL: Creating AMIs and Other AWS Stuff"
date:   2018-06-27 20:15:00 -0000
categories:
  - Coding
tags:
  - aws
---
I spent some time this afternoon at work doing some reading and playing around with AWS. I had heard of AMI's mentioned before in the documentation, and knew they could be used to create some sort of image, but that's where my knowledge stopped on the matter. So I took the time to investigate and see what I could find out.
## AMIs
AMI's are essentially images of the core system that you can save off and use to generate a new instance. I don't know if this is a good comparison or not, but it's kind of like creating your own packaged distribution. You can start with one of the base AMI's offered through amazon (amazon linux, RHEL, Ubuntu, etc), install any additional packages/tools/applications, and then create your own personal AMI based off of that installation.

The dashboard makes this super simple. After you've got your base EC2 instance setup the way that you want it to be, all you need to do is stop the instance and then select to create an image. This will create an AMI from that stopped instance and save it to your AMI list.

The next time that you go to spin up a new instance, that AMI can be selected from the list of images at deployment time. This saves you the hassle of having to install packages on every deployment. Pretty nice.

## Changing EC2 Size
There's also a built in option in the menu to adjust the size of an existing EC2 instance, say from like a `T2.micro` to a `T2.medium`. However, in order to do the migration, you will have to power down the machine before having the option to select the migration. This was kind of a no go in my instance, as I didn't want to lose the IP address assigned to my existing box. So I opted to go with the AMI route and spin up a new box.

## EC2 Pricing Mystery
For as much as people really love AWS, I find the pricing model to be maddening. The fact that the `T2` type instances are what's available for most basic things, but that you can't actually use the instance at any sort of real load is just crazy to me.

The `T2` type instances all use this credit system. If you go over a certain percentage of CPU usage, you start spending credits to keep the performance going. Once you drop back down below that threshold, you start to accrew those credits again. The idea is that the boxes should only be used for bursty traffic, and nothing at any type of load.

...But what about my case where 4 CPUs is overkill? Why should I need to pay for that much hardware just so that I don't get throttled for running at or above 30% CPU? It seems crazy to me, I really don't understand it...

💚