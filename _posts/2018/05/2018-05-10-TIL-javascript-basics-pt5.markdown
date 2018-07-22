---
layout: post
title:  "TIL: Javascript Basics: Part 5"
date:   2018-05-10 20:35:00 -0000
categories:
  - Coding
tags:
  - javascript
---
Not really feeling it today so I didn't get as much done as I would have wanted to. A lot of my learning was project specific to work today, so unfortunately I can't really share that information. Had a lot to do with security and how we handle users, which was actually pretty neat to learn about.

Also, as a bit of a side tangent, today was end of week 2 of the couch-2-5k program for my girlfriend and I. Two weeks of running and it's all getting much easier. I'm actually getting to the point where I look forward to my next run, which is something I never tought I'd say... ever.

Anyways, today was the start of DOM manipulation using purely javascript. One of the main reasons I wanted to go take this course was because it took you away from using jQuery for everything. jQuery makes things simple, but I've always felt like it's also overboard for many things.

So, here are those notes from today's lesson:

```js
let val;

// Baisc document items
val = document;
val = document.all; // gives a collection of all items on page
val = document.all[0]; // give the tag and its contents from the collection
val = document.all.length; // returns the number of elements in the DOM
val = document.head; // returns head tag
val = document.body; // returns body tag
val = document.doctype; // returns doctype
val = document.domain; // returns current domain
val = document.URL; // returns current URL
val = document.characterSet; // encoding for the page
val = document.contentType; // content type of the page

// selecting items without using selector
// This is not recommended
val = document.forms; // returns array(collection) of forms
val = document.forms[0]; // collection can be referenced by location
val = document.forms[0].id; // reutrns id property of the form
val = document.forms[0].method; // returns method value of the form

// Get collection of links
val = document.links;
val = document.links[0];
val = document.links[0].className; // String of all of the related classes
val = document.links[0].classList; // Gets a DOMTokenList of classes
val = document.links[0].classList[0]; // gets the specific class

// Get collection of images
val = document.images;

// Get collection of scripts
val = document.scripts;
val = document.scripts[2].getAttribute('src'); // gets the src sttribute of the 3rd script found

// You CANNOT use a forEach for a collection. Must convert to array first!
let scripts = document.scripts;
let scriptsArr = Array.from(scripts);
scriptsArr.forEach(function(script){
    console.log(script);
});

console.log(val);
```

💚