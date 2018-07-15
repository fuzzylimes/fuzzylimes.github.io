---
layout: post
title:  "TIL: Clean Way of Resetting NodeJS Console"
date:   2018-07-15 10:55:00 -0000
categories: TIL
---
This issue has haunted me for over a week now. Just when I thought I'd figured out the answer, I found more problems with the solution. But I've finally stumbled across an anwer that's exactly what I wanted.

Found on [this gist here](https://gist.github.com/timneutkens/f2933558b8739bbf09104fb27c5c9664), this is a relatively straight forward way of cleaning up the console completed and getting it ready for new writes. In my case, it's the perfect way to clear it console between each write update when writing stats out.

💚