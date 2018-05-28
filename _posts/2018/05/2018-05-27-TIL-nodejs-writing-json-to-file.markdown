---
layout: post
title:  "TIL: Writing JSON to file with Nodejs pt1"
date:   2018-05-27 21:15:00 -0000
categories: TIL
---
Marking this entry as part one as I don't have much time tonight to work on this. Today was a break for me. Lots of relaxing and doing other things outside of worring about work or other projects. Much needed.

Though I did sit down for a bit tonight to learn how to easily write JSON to a file using nodejs. This is very similar to the reading values in from a JSON file post that I made last week, only doing the reverse.

This again uses the `fs` module to access the file system. All you need to do is to convert your object to a string using `JSON.stringify()`, then write it into the file like shown below:

```js
const fs = require('fs');

let a = {
    name: 'Bob',
    age: '42'
}

fs.writeFileSync('sample.json', JSON.stringify(a, null, 2));
```

This will either create a new file named `sample.json` if it doesn't exist, or overwrite the existing with the object.

💚