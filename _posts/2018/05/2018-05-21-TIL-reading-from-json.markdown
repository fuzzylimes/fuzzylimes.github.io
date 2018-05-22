---
layout: post
title:  "TIL: Reading from JSON in NodeJS"
date:   2018-05-21 20:15:00 -0000
categories: TIL
---
I don't have much time as I'm currently working on my main project for work, but I wanted to take a minute to talk about reading in json files in nodejs.

All of these great info is documented in this [original blog post](https://www.codementor.io/codementorteam/how-to-use-json-files-in-node-js-85hndqt32).

For all of these examples, we'll use a dummy json file with the following content:

```json
{
    "name": "test",
    "id": 1234
}
```

## Automatically Reading JSON file
This is probably the absolute easiest way to read in a json file and make it a useable object. All you need to do is simply require the file and assign it to a variable:

```js
var obj = require('./sample.json');

console.log(obj.name);
```

## Using file system
The other way is by using the file system `fs` module. This requires many more steps for the same result:

```js
const fs = require('fs');

let contents = fs.readFileSync("./sample.json");
let jsonContent = JSON.parse(contents);

console.log(jsonContent.name);
```

💚