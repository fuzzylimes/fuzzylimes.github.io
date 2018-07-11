---
layout: post
title:  "TIL: The correct way of adding text to an element"
date:   2018-07-10 20:40:00 -0000
categories: TIL
---
My work with javascript over the last two days has led me to finally learning how to manipulate the DOM with javascript on the client side. I think my entire last project was all server side rendered, so I didn't have to worry about any of that kind of stuff. But now that my `ute-visor` project relies on updating the page based on passed data through the socket, I'm having to finally learn it.

Today I learned taht there's a more correct way of adding text to a found element rather than just setting the `innerHTML` to a value. Evidently doing things that way leads yourself to potential security risks.

So to avoid those potential issues, the correct way of doing it is as follows:
```js
var span = document.getElementById(server + '-status');
var txt = document.createTextNode('RUNNING');
span.appendChild(txt);
```
This will create a new text node and add it to the selected element.

💚