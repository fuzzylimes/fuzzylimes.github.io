---
layout: post
title:  "Weekend Update"
date:   2017-12-17 21:45:00 -0500
categories: python
---
Pretty productive weekend for me this week, nearly got everything done that I wanted to. After getting some minor fixes into my twitch scraping tool this week, I wanted to move ahead with my overall project and start playing around with html report pages.

I'd previously created a neat little html report generator for work and I figured I'd kind of do the same thing with this. My goal would be to generate a new for each stream that is tracked. The page would be a clean looking UI that would show all of the games played during a streaming session, the length of the stream, and the max viewers/chatters throughout the time playing the game.

### Responsive/Mobile First
I wanted to make sure that whatever I did would look good both on mobile and on desktop... so I went the easy route and picked bootstrap as my base. Since my background on web design is meh and I really didn't want to spend my whole weekend prototyping a page, bootstrap was my easy solution.

### Basic design
I knew I wanted to have a small header at the top for the streamers name/link to stream/profile pic. This turned out looking like so:

![User section]({{ "/assets/img/2017-12-17-1.png" | absolute_url }})

Next was the content. I decided that I'd do just a simple card setup. Cards would have a date and time as the header, and then a list of box art in the order that the games were played:

![Game cards]({{ "/assets/img/2017-12-17-2.png" | absolute_url }})

The cards themselves can be clicked to expand and reveal more stats for each of the games:

![Game card details]({{ "/assets/img/2017-12-17-3.png" | absolute_url }})

### Moving on
There are lots of little things that I want to change, like making it so that the logged start/end times are actually relative to the stream, not so much the actual time (maybe add an extra field for this?). I also need to work out the roll over for each of the logs so that there's one log for each month per user. That way the generated html pages will still be manageable in size.