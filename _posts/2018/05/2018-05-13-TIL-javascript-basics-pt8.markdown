---
layout: post
title:  "TIL: Javascript Basics: Part 8"
date:   2018-05-13 20:30:00 -0000
categories: TIL
---
Still not really feeling it today but still managed to make it through a few more modules. Still just more basic Javascript stuff dealing with the DOM. Lacking motivation so another low effort post today. Starting to feel guilty about all the copy paste.

## Creating Elements
```js
// Creating elements

// Create element
const li = document.createElement('li');

// Add class
li.className = 'collection-item';

// Add id
li.id = 'new-item';

// Add attribute
li.setAttribute('title', 'New Item');

// Create text node and append
li.appendChild(document.createTextNode('Hello World'));

// Create new link element
const link = document.createElement('a');
// Add classes
link.className = 'delete-item secondary-content';
// Add icon html
link.innerHTML = '<i class="fa fa-remove"></i>';
// Append link to li
li.appendChild(link);

// Append element as child to ul
document.querySelector('ul.collection').appendChild(li);

console.log(li);
```

## Removing and Replacing Elements
```js
// Replace element

// Create an element
const newHeading = document.createElement('h2');
// Add id
newHeading.id = 'task-title';
// New Text Node
newHeading.appendChild(document.createTextNode('Task List'));

// Get the old heading
const oldHeading = document.getElementById('task-title');
// Get the old heading's parent
const cardAction = document.querySelector('.card-action');

// Replace
cardAction.replaceChild(newHeading, oldHeading);


// Remove an Element
const lis = document.querySelectorAll('li');
const list = document.querySelector('ul');

// Remove list item
lis[0].remove();

// Remove child element
list.removeChild(lis[3]);


// CLASSES and ATTRIBUTES
const firstLi = document.querySelector('li:first-child');
const link = firstLi.children[0];

let val;

//Classes
val = link.className; // String of class names
val = link.classList; //DOMTokenList (linke an array)
link.classList.add('test');
link.classList.remove('test');
val.add('testing'); // val is already set to link.classList, can just use val for assignment

// Attributes
val = link.getAttribute('href');
val = link.setAttribute('href', 'https://google.com');
link.setAttribute('title', 'Google');
val = link.hasAttribute('title'); // check to see if the element has a specific attribute
link.removeAttribute('title');

console.log(val);
```

💚