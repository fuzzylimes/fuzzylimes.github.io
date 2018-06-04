---
layout: post
title:  "TIL: Setting MongDB to Automatically Delete Records"
date:   2018-06-03 20:55:00 -0000
categories: TIL
---
As part of the next project I need to complete at work (actually should have completed this weekend, oops), I'm going to need to be purging data from a MongDB pretty regularly (thinking every week or so) in order to keep the db from getting to large. The applcation in question is just used for test and holding test data so, I don't need any crazy data retention in it. And it will be storing upwards of 14mil new pieces of data a day so... it needs to be cleaned out.

My search for cron jobs to keep it cleaned up [led me to a post](https://forums.meteor.com/t/solved-remove-old-documents-periodically-good-way-of-doing-it/6853/4) that referenced using built in mongo functionality to cleanup old records. A quick google search brought me to [the offcial documentation](https://docs.mongodb.com/manual/tutorial/expire-data/) where they fully outline how to use this functionality.

I've yet to try this yet (task for tomorrow at this point) but it appears that it supports two means of setting a time-to-live value:
1. Number of seconds after which to be marked as expired and removed
2. Time/Date after which to be marked as expired and removed

They both pretty much work in opposite ways. For the first, you set your collection to mark records as expired after a certain number of seconds since creation, and supply the creation time in the record.

For the second, you define the collection to be mark records as expired after 0 seconds, then supply an expired at time in the record.

Both ultimately achive the same thing, and I'm assuming that they both have similar performance impacts.

💚