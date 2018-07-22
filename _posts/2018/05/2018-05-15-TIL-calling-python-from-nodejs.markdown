---
layout: post
title:  "TIL: Launching Python from NodeJS"
date:   2018-05-15 20:20:00 -0000
categories:
  - Coding
tags:
  - node.js
---
Continuing work on my side project/project needed for work, I ran into a situation where I needed to kick off a python script from an express and get the output back. Essentially I need python to run a selenium script for me and retrieve a specific piece of data after doing some login stuff. To my surprise, it was easier to get working that writing the selenium script.

My google searching led me to [this post](https://medium.com/@HolmesLaurence/integrating-node-and-python-6b8454bfc272) which explained a few different ways to launch a python script from within a node app. As I'm not picky at the moment and just need it to work, I went with the most basic, out of the box option.

Lets assume that I have a simple python script that does nothing but add two numbers and print them out:

```python
a = 5+5
print(a)
```

If I were to want to run that script, and get the output from it, all I need to do is ensure that it's printing to stdout, and I'll be able to grab it.

Then, in the node app, we create a child process to run the script which will read from standard out after the script has completed:

```js
app.get('/maths', maths);

function maths(req, res) {
  var spawn = require("child_process").spawn;
  var process = spawn("python", ["./maths.py"]);
  process.stdout.on('data', function (data) {
    res.send(data.toString());
  });
}
```

Easy as that, you've got your output back into the file. Note that I did run into some buffer issues when doing it, so this is really best to break up your print statements (printing a large dictionary for me was a no go). But you can easily set that response to a variable and use it as needed:

```js
app.get('/maths', maths);

function maths(req, res) {
  var spawn = require("child_process").spawn;
  var process = spawn("python", ["./maths.py"]);
  process.stdout.on('data', function (data) {
    let a = data.toString().split('\r\n');
    res.send(`Here's the data I found: ${a[0]}`);
  });
}
```

💚