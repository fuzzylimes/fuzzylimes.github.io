---
layout: post
title:  "TIL: More about Cookies"
date:   2018-04-02 20:45:00 -0000
categories:
  - Coding
tags:
  - web development
---
Tonights activies were focused on more Go training, all of which was centered around the topic of sessions and state in web apps. So a lot of this again was dealing with cookies, rather than JWT. I'm not sure if JWT hadling will be covered in this course or not, but at least it's giving me a chance to learn more about cookies.

## How cookies (generally) work
This was all news to me. I new that cookies were used for some sort of session, but that was all I really knew.

So cookies are basically some unique identifier that the server will assign to you for your session. That cookie gets stored both on the server as well as returned back to the client. Whenever you browse a page, you're sending that cookie back to the server for verification, which is what grants you access to the content that you can see. This unique id that's assigned to you is in a temporary database, seperate from where your user information is at, and typically links back over to your user data. When the session has expired, your cookie is killed and it's removed from the temporary database.

And that's all there really is to it. Two different database tables. One has temporary session information that links back to your saved information. Session information gets cleared out from the server and from your browser when cookies are expired.

To handle the unique id values, the lession's tonight took advantage of the `github.com/satori/go.uuid` package. It allows for simple uuid generation in 5 different ways (only one used in the videos, didn't bother to read up on the rest). To generate a uuid, you only need assign a variable with a short method call:

```golang
sID, _ := uuid.NewV4()
fmt.Println(sID.String())
```
String will convert the generated uuid back into a usable string that could be inserted into your cookie (i.e. the Value field).

Doing some reading on my own comparing cookies to JWT tokens, it seems that cookies have higher security risks related to cross site scripting attacks. They're also more focused on browser interaction rather than using an API to access data, which is probably why I've never seen them in any of the other REST API lessons that I've done.