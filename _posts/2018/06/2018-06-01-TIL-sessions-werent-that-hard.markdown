---
layout: post
title:  "TIL: Session Weren't That Hard"
date:   2018-06-01 20:05:00 -0000
categories: TIL
---
The first itteration of my side project at work is finally finished. I was able to get sessions working just as I had always imagined them working, and it's such a beautiful thing. Oh, and I was making them way harder than they needed to be.

Looking back I think my biggest issue was just not understanding what the `express-session` package was providing and how it was working. Maybe I didn't read the documentation enough, but I was missing out on the whole bit where it really does take care of everything for you. Seriously. There's nothing you need to do with checking your session ids, or reading in your cookies. It does it all for you without any effort at all.

If you want to attach or assign a new property or value to the session, it's really as easy as adding a `.value` to the `req.session` object, and bam: new property. And that property will then be accessible from anywhere where the `req` object is passed. This greatly simplified my code as I was able to pass the associated credentials along with the req as it moved throughout my application.

For my initial work, I didn't get into anything crazy like working with passport as I didn't need to deal with logins, nor did I have a backend to setup. However, I can see how easily all of that would fit in when using sessions.

Cool stuff, I'm glad I'm past that mental road block.

💚