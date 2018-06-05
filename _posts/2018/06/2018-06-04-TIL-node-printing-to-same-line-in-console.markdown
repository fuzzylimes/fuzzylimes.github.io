---
layout: post
title:  "TIL: Printing to same line in console with Node"
date:   2018-06-03 20:55:00 -0000
categories: TIL
---
Tonight I learned a trick for doing something that I've wanted to know how to do for a while now: updating the same line on the console/stdout when printing data. You know, kinda like you see when you're installing packages and such.

Turns out it's actually pretty straight forward. I found a couple different ways that suggested doing it, but the following way worked flawless for me without any issues.

You'll first need to import the `process` module. Once imported, you'll be creating the following set of calls:

```js
process.stdout.clearLine();
process.stdout.cursorTo(0);
process.stdout.write(`Loop number ${count}`)
```

What this will effectively do is clear out the line of stdout that's being displayed to the console, move the cursor back to the start, and then write the new output to the console. So if you put the above in a loop, incrementing `count` each time, rather than see something like:

```
Loop number 1
Loop number 2
Loop number 3
Loop number 4
Loop number 5
```

You would just see:

```
Loop number 5
```

💚