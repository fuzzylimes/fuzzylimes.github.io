---
layout: post
title:  "Twitch Project Update"
date:   2017-12-05 19:15:00 -0500
categories: python
---
Just another minor follow up to the project that I had started yesterday. Not too much to report, but I do have it in a state where it's ready to be used.

Wrapped up my first itteration of the program tonight. Added in some additional functionality that would handle offline streams. I made the decision that I wanted to go ahead and log the status of streams throughout the day, and not just when they were online like I had initially planned.

I also decided to make my life much easier and change the way the program runs. Initially I had planned to make it so that the tool would run all of the time, polling channels on 15 minute intervals until they were found to be online, then poll every 5 minutes until they went offline. As soon as I got into bed last night, I realized that's waaaaaay too much work for what needed to be done.

Instead, I opted for using the power of cron jobs and just allow the script to be run every 5 mintue. That will allow for me to gather 12 data points for my selected streams every hour, 24 times a day. That way I could track trends for when streams actually go online, how long they stay on for, what the viewer trends look like, etc.

Once again, all of the files have been updated and are available [here](https://github.com/fuzzylimes/New_Twitch_API_Channel-Stat-Scraper). I'll probably revisit the project in another week or so to implement log rollover at the end of each month.