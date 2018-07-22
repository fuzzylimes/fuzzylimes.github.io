---
layout: post
title:  "TIL: Setting cron jobs from Node"
date:   2018-06-05 20:55:00 -0000
categories:
  - Coding
tags:
  - node.js
  - cron
---
Here's a neat little trick/hack I learned today for being able to quickly control crontab jobs from routes in your node application.

In my case, for testing purposes, I wanted to be able to control when my simulator kicked off traffic without having to log into the box and manually change the file. So I had the idea of adding in two additional routes that would modify the crontab file on the test box: `/cronjob/enable` and `/cronjob/disable`.

The goal for this was simple. Create two different txt files, one empty file called `clear.txt` that would be used to clear the jobs, and another called `cron.txt` that contained the cron tasks I wanted created.

Cron jobs can be added to crontab by using the following format: `crontab <filename>`. So the goal now was to be able to send these commands to the command line.

To do so, you can use the following with `child-processes`:

```js
const { exec } = require('child_process');
exec('crontab clear.txt', (err, stdout, stderr) => {
  if (err) {
    console.log('Unable to clear cron jobs!');
  } else {
      console.log('Crontab cleared.');
  }
});
```

And repeat the process on the route for adding the cron job with its respective cron `.txt` file.

💚