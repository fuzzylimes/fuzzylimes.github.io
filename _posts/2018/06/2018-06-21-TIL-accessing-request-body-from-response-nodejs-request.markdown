---
layout: post
title:  "TIL: Accessing Request Body from Response using nodejs Request Package"
date:   2018-06-21 20:25:00 -0000
categories:
  - Coding
tags:
  - node.js
---
This is one of those things where the answer was so obvious that I spent 2 hours looking for a different answer before finally realizing it was right in front of me all along. For a while now I've been trying to figure out if it was possible to access the request content in the response call back when using the `request` package in nodejs. I thought it would be a pretty common question, but evidently only me and 2 other people have ever asked it (or we're both just really bad at reading the documentation).

For me, I needed to be able to correlate messages along a call flow. In order to do so, I needed to be able to log a record when my response came back. The problem was, I also needed to log off part of what was in the initial request message.

Turns out, you can access all of the request object right inside the response! Yeah, go figure. `response.request` will get you access to a whole slew of things, like `response.request.uri.path`, `response.request.body`, `response.request.headers`, you name it!

Here's a simple little program I put together to demonstrate it:

```js
const express = require('express');
const request = require('request');

const app = express();
const port = 5555;
app.use(express.json())


app.post('/', (req, res) => {
    res.setHeader('Content-Type', 'application/json');
    console.log(JSON.stringify(req.body));
    request({
        url: `http://localhost:${port}/testing`,
        headers: {'Content-Type': "application/json", 'Something-random': '123'},
        body: JSON.stringify(req.body)
    }, (error, response, body) => {
        console.log(response.statusCode);
        console.log(response.request.uri.path);
        console.log(response.request.headers);
        console.log(response.request.body);
        res.send(body);
    });
    console.log("I get hit first");
});

app.get('/testing', (req, res) => {
    res.setHeader('Content-Type', 'application/json');
    res.send({id:1234});
});

app.listen(port, (err) => {
    console.log(`Server started on ${port}`)
});
```

You can run the test by sending something through curl, like `curl -X POST http://localhost:5555/ -H 'Content-Type: application/json' -d '{"email":"test@test.com", "password":"password"}'`.

💚