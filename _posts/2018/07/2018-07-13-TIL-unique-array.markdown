---
layout: post
title:  "TIL: Unique Array in JS"
date:   2018-07-13 20:40:00 -0000
categories:
  - Coding
tags:
  - javascript
---
Today I finally needed to make a unique array in javascript. For some reason I've never had to do that until today... go figure.

The first searches I took brought me to an older answer which has you using `filter` to build the unique array:
```js
var a = ['a', 1, 'a', 2, '1'];
var unique = a.filter( function(value, index, self) { 
    return self.indexOf(value) === index;
} );
```

Which works just fine... but it's pretty ugly looking.

Then I searched some more and found out that the added a `Set` method in ES6:

```js
var myArray = ['a', 1, 'a', 2, '1'];

let unique = [...new Set(myArray)]; 
```
This one is much cleaner.

💚