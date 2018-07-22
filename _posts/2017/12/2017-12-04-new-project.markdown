---
layout: post
title:  "New Project: Twitch.tv channel stat scraper"
date:   2017-12-04 20:30:00 -0500
categories:
  - Coding
tags:
  - python
---
Short update as I need to get myself to bed. After feeling overwhelmed/burnt out from all of the front end development I'd ben working through, I decided to take a break and do a fun side project. What I landed on was a bit of a scraping project that will periodically pull statistics from Twitch streamers and store them into some sort of data structure.

For the intiial phase, all data will be written into csv files. They will then be rotated out at the end of the month and hypothetically be available for anyone to have access to them.

The plan is to accept a list of twitch channels that you wish to monitor. The program will then poll the channels every 15 minutes to see if they are live. If they are live, they will then be polled every 5 minutes and their statistics saved off into a csv file. Once it is detected that the channel is no longer live, the polling will return to 15 minutes.

Tonight I was able to get all of the base logic done to handle the polling and saving to the csv files. I hadn't ever used the csv.DictWriter before tonight, and it was surprisingly easy to do. All of the code can be found in my repository [here](https://github.com/fuzzylimes/New_Twitch_API_Channel-Stat-Scraper).