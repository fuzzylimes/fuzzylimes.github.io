---
layout: post
title:  "TIL: Easy Way of Passing Data Between ExpressJS Paths"
date:   2018-05-16 19:25:00 -0000
categories: TIL
---
Learned a neat little trick this morning for passing data between two different paths when using express in a node project. This came up when I was trying to figure out how I'd be able to return data that was retrieved during a form post and move back into the the main index page after redirect.

My first instict was to use the redirect method, but after reading up on it I found that all it can really do is redirect. There wasn't really a way to redirect WITH some sort of data, other than lumping it into an ugly query string which I wasn't going to do.

And then I found a suggestion to use the `next` parameter. While this probably isn't the way it was intended to be used, it sure does make passing the values very simple.

Lets take a look at this very simple express server:

```js
const express = require('express');
const app = express();

function homePage(req, res) {
    if (req.dataProcessed) {
        console.log(req.dataProcessed);
        res.send(req.dataProcessed)
    } else {
        console.log('No data found');
        res.send('Not Found');
    }
}

function testing(req, res, next) {
    req.dataProcessed = 'I made this';
    return next()
}

// Index Route
app.get('/', homePage);
app.post('/test', testing, homePage);

const port = 5000;

app.listen(port, () => {
    console.log(`Server started on port: ${port}`);
});
```

The key here is with the post to the `/test` path. In this case, we set it up with two different function calls: the initial function for the `/test` path, and the next endpoint to hit when calling `next()`.

In this case, if a GET request is sent directly to `/`, a `Not Found` response is returned. However, if the POST is sent to `/test`, the `req.dataProcessed` value gets set and then passed on to the home page function. `req.dataProcessed` is then available for use within that function, which causes the value of `req.dataProcessed` to be returned.

Planning on implementing this method when returning back generated user tokens back to the client.

💚