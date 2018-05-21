---
layout: post
title:  "TIL: Making Requests in NodeJS"
date:   2018-05-20 21:20:00 -0000
categories: TIL
---
Today I finally got requests working from within my node app. I don't know why I was making this processes so much harder than it needed to be. All of it runs async, all the values can be passed around, and it works just like you would think it would.

The secret sauce for me getting this to work was by first installing the `request` package from npm:

```
npm install request --save
```

With requests installed, you can import into your app just like normal:

```js
const request = require('request');
```

From there, it's as easy as making a request:

```js
request(`http://localhost:${port}/testing`, (error, response, body) => {
    res.send(body);
    console.log(response.statusCode);
});
```

Setting up in this way gives you both the response, which is where things like your headers and response code are stored, as well as the body. You can then do with it as you like.

So in my simple app, I set it up so that sending a GET request to `/` would send another get request to the `/testing` path within the same server app. This endpoint responds back with a json payload, which is finally passed back to the user. Here's the full code of my short session tonight:

```js
const express = require('express');
const request = require('request');

const app = express();
const port = 5555;

app.get('/', (req, res) => {
    res.setHeader('Content-Type', 'application/json');
    request(`http://localhost:${port}/testing`, (error, response, body) => {
        res.send(body);
        console.log(response.statusCode);
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

Much more information and more indepth examples can be found on the request package's [github page](https://github.com/request/request).

💚