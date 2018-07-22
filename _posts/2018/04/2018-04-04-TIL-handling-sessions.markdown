---
layout: post
title:  "TIL: Handling Sessions"
date:   2018-04-04 21:00:00 -0000
categories:
  - Coding
tags:
  - web development
---
Tonight was learning more about some theories behind handling sessions in your websites/applications. This continues to build on the lessons from the last few days with cookies.

## Handling Session timeout
Theres a really simple way of handling time outs, and that's to keep an extra time value logged along with the unique session information in the server side db. Basically any time that a user browses around your site, you'd update the session with a new time on the DB side to keep the session alive, and set a new expiration time on the client's cookie.

If the user goes away for a while and the MaxAge of the cookie expires on the client, the next request will fail. They'll have to log back in, get a new cookie, and set a new session value on the server side. It's a pretty simple method, but it makes a lot of sense conceptually.

## Handling Expired Sessions
There's always a possibility that old sessions will get stuck around in the DB. Another easy way to handle this is to write a simple script that would run through the objects in your db and handle the cleanup of anything that's been passed expired.

The other simple method that was shown in the lectures was connecting a cleanup with the logout button. So in someone were to actually log out from the site, trigger off our cleanup script to cleanup any sessions they may have left behind from their visit.