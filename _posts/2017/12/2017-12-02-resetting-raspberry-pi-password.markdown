---
layout: post
title:  "Resetting Raspberry Pi Password"
date:   2017-12-02 11:45:00 -0500
categories:
  - Tech
tags:
  - raspberry pi
---
I'd picked up a pi a few months back thinking it would be a fun little weekend project. After setting it up, setting a static IP, and setting up ssh on my phone, I forgot all about it. Fast forward a few months, and surprise, I couldn't remember my password (I'd changed from default and of course didn't write it down).

I've forgotten linux passwords in the past. That usually required doing some fancy stuff at boot time, hacking around to reset the password that way, but the Pi doesn't seem to work that way. From googling around it appeared that I needed to power down, pull out the card, edit a boot file, put it back in, then reset the password. All of the "guides" I found had the same set of steps, all of which were partially correct and got me to the same spot.

A hour of frustration later, I finally found my missing piece and got my password reset. Here's a nice end of 2017 guide for resetting the password:

---

## 1. Power off and remove the sd card
Go ahead and power off the pi and take out the sd card. You'll need to put it into your computer to edit a file

## 2. Edit the `cmdline.txt` file
Open up the `cmdline.txt` file in your favorite editor. We need to add in a line that will force single user mode. Add `init=/bin/sh` to the end of line in the file so that it looks something like this:
>dwc_otg.lpm_enable=0 console=ttyAMA0,115200 console=tty1 root=/dev/mmcblk0p2 rootfstype=ext4 elevator=deadline rootwait init=/bin/sh

## 3. Put the sd card in and boot
Plug the sd card back in and plug in the power.

## 4. Enter into root prompt
When turned back on you'll see a bit of scrolling before stopping at an empty line. Hit return a few times and you should see a plain `#` prompt. At this point you'll need to make sure you have a wired keyboard plugged in (in my case my wireless keyboard was not working). Enter `su` to enable the root prompt (no password required in my case)

## 5. Mount root
Before being able to change the password, you'll need to mount the root directory. In my case, this is the path in the `cmdline.txt` file set equal to the `root` value:
>root=/dev/mmcblk0p2

To mount you'll need to use the following: `mount -rw -o remount /dev/mmcblk0p2 /`, where mmcblk0p2 is the value from the root path.

## 6. Reset password with passwd pi
Send the command `passwd pi` and set your password to something new. Then promptly write it down :)

## 7. Return the `cmdline.txt` file to the previous state
Power down the pi, unplug the sd, and then edit the `cmdline.txt` file to pull out the single user init line that was prevously added.

## 8. Done
Plug the card back in and power it back up. You should now have use of the pi user once again.

---

Hopefully this can help save you some time. The resources I used it getting this working can be found below:

* [Reset password 1](http://mapledyne.com/ideas/2015/8/4/reset-lost-admin-password-for-raspberry-pi)
* [Reset password 2](https://howtoraspberrypi.com/recover-password-raspberry-pi/)
* [Geting the correct boot path](https://www.raspberrypi.org/forums/viewtopic.php?t=193816)