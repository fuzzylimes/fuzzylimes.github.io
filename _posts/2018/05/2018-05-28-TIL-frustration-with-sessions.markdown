---
layout: post
title:  "TIL: Sessions: I Don't Know What I'm Doing"
date:   2018-05-28 20:40:00 -0000
categories: TIL
---
I spent a good chunk of time today playing with and reading documentation for sessions. Just when I thought I was starting to get a grasp on what I'd need to do to handle my scenarios, I'd come across something that would completely contradict what I'd been reading. That's starting to wear on me a little bit.

I think my main confusion lies in what all is being handled for me by the node modules that I'm loading into the program. Like is express-sessions handling everything that I'd need for me? Do I not need to take what it makes and create some other database/table style storage for the data? Can I just let it handle all of that for me?

I really want to play around with that a little more tonight and see if I can make a little more sense out of it. I don't like feeling completely stumped on a topic expecially when I've been feeling like I'm so close to solving it out.

My susspicion is that I'm once again making things way too difficult on myself, and that the session module really does handle everything I need. Storing all of the sessions and their keys for me, which would just leave the look up to a secondary file at session creation time... But then I don't know what I'm doing to restrict routes based on the cookie... and now I'm just rambling.

Frustrating day, didn't get nearly to the point where I wanted to be. Grr.

💚