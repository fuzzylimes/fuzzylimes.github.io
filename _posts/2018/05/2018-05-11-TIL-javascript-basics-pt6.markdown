---
layout: post
title:  "TIL: Javascript Basics: Part 6"
date:   2018-05-11 12:15:00 -0000
categories: TIL
---
I've come down with some kind of cold today, not really able to focus like I wanted to this morning. Very short lesson session before heading to lie down. Today was starting with single element selectors, more super basic stuff dealing with DOM items.

```js
// Single Element Selectors
// Will only grab the firt instance of an item found if multiple exist
// Multiple Element Splectors will returns collections of items found

// document.getElementById() - selects an element by its id tag
let val;
val = document.getElementById('task-title');
console.log(val);

// Get things from a found element
console.log(val.id); // get id of element
console.log(val.className);
console.log(val.textContent); // Get the text of the tag

// Change styling - anything you can do with css, you can do here
// You'd still do your styling in css though, don't use this
val.style.background = 'red'; // change background color
val.style.color = 'green'; // change text color
val.style.padding = '5px'; // increasing padding of element
// val.style.display = 'none'; // hide an item

// Change content
val.textContent = 'Task List';
val.innerText = 'My Tasks';
val.innerHTML = '<span style="color:blue">Task List</span>';

//document.querySelector()
let val2 = document.querySelector('#task-title');
console.log(val2);
console.log(document.querySelector('.card-title'));
console.log(document.querySelector('h5'));

document.querySelector('li').style.color = 'red';
document.querySelector('li:last-child').style.color = 'red';
document.querySelector('li:nth-child(3)').style.color = 'yellow';
document.querySelector('li:nth-child(4)').textContent = 'yellow';
document.querySelector('li:nth-child(odd)').style.background = 'pink';
document.querySelector('li:nth-child(even)').style.background = 'green';
```

💚