---
layout: post
title:  "TIL: Quick rounding in JS"
date:   2018-07-12 20:40:00 -0000
categories:
  - Coding
tags:
  - javascript
---
In the past I'd always used the `Math.round()` function with floor and such to handle rounding to decimal places, turns out there's a much simpler way of doing it...

To round to say 3 decimal places, just use the `toFixed()` method that's available to any `Number`. For example:
```js
a = 12.34567
a.toFixed(3);
```
The above will return `12.346`, where the method automatically rounds up the value for you.

This is much shorter than the way I'd been doing the math in the past.

💚