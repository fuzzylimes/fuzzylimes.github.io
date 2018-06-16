---
layout: post
title:  "TIL: Javascript Classes"
date:   2018-06-15 23:40:00 -0000
categories: TIL
---
I finally used Javascript classes today for the first time. While porting over one of my tools to nodejs, I had the oportunity to implement a class with a constructor to better manage object data. Turns out using Javascript classes is super simple, there's really not much to them (granted I didn't do anything fancy with sub-classes and such).

```js
class Turtle {
  constructor (color) {
    this.color = color;
  }
}
```

💚