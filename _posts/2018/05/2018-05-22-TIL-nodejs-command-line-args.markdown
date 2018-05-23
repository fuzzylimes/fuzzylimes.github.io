---
layout: post
title:  "TIL: NodeJS Command Line Args"
date:   2018-05-22 21:10:00 -0000
categories: TIL
---
Once again, don't really have any time to write tonight. Completely overwhelmed with work, brain is melting. I did learn a neat little trick for reading in command line arguments in Node though, so I guess I'll share that.

Nothing crazy needed to be imported, works fine with the standard lib. All you need to do is to use `process.argv`. This creates an array of all of your command line arguments, including your initial `node` and `path` parameters.

For example, the following command `node test.js param1 param2` looks like this in array form:

```js
node sample.js
node sample.js param1 param2
[ 'node',
  'sample.js',
  'param1',
  'param2' ]
```

💚