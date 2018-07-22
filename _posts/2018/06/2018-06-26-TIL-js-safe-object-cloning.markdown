---
layout: post
title:  "TIL: Safe Cloning in JS"
date:   2018-06-26 20:52:00 -0000
categories:
  - Coding
tags:
  - javascript
---
While working more on my React lessons tonight, I learned a helpful hint for ensuring that a new copy of an object gets created rather than just creating a new reference to the original object.

The lesson focused on the newer ES6 way of dealing with this using the new `spread` functionality.

Lets assume that you have an array like so: `let fruits = ['apple','banana','grape']`

If you wanted to make a copy of that array, you could use the spread method like so:

```js
let fruits = ['apple','banana','grape']
const myFruits = [...fruits]
```
This will create a brand new array from the original. Any changes then made to the duplicate will not update the original.

This same functionality can be applied to javascript objects as well:
```js
let person = {
    name: 'Bob',
    age: 45
}
const myPerson = {
    ...person
}
```
This will take all of the properties of the `person` object and add them into the new `myPerson` object.
💚