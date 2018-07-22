---
layout: post
title:  "TIL: Javascript Basics: Part 7"
date:   2018-05-12 20:15:00 -0000
categories:
  - Coding
tags:
  - javascript
---
More Javascript DOM stuff today, and nothing that's really that exciting. All of the basic stuff is starting to slow me down, I feel my eyes starting to glaze over again, something that I'd complained about a few weeks back. I think I need to start creating better summary notes as I get done with sections, so that'll be coming in the next few days.

Today is more DOM manipulation items. I'm about halfway through these sections, so there's still plenty more of this to come, for better or worse. Like I said, it's starting to drag and I'm losing focus/interest again...

## Multi Element Selectors
```js
// Multi element selectors
// Creates a collection or node list

// document.getElementsByClassName()
let items = document.getElementsByClassName('collection-item'); // creates a collection of each of the collection-item class elements
console.log(items);
console.log(items[0]); // returns the first list item
items[0].style.color = 'red';
items[3].textContent = 'Hello';

// Can also look local by chaining queries
const listItems = document.querySelector('ul').getElementsByClassName('collection-item');
console.log(listItems);

// document.getElementsByTagName
let lis = document.getElementsByTagName('li');
console.log(lis);
console.log(lis[0]);
lis[0].style.color = 'blue';
lis[4].textContent = 'ASDF';

// Not a true array, so array functions will not work on it. Have to convert it to an array first
lis = Array.from(lis);
lis.reverse();
console.log(lis);
lis.forEach(function(li, index){
    console.log(li.className);
    li.textContent = `${index}: Hello`;
});

// document.querySelectorAll()
items = document.querySelectorAll('ul.collection li.collection-item'); // Returns a NodeList object

items.forEach(function(item, index) {
    console.log(item.className);
    item.textContent = `${index}: Hello`;
});

const liOdd = document.querySelectorAll('li:nth-child(odd)');
const liEven = document.querySelectorAll('li:nth-child(even)');

liOdd.forEach(function(li, index) {
    li.style.background = 'grey';
});

for (let i = 0; i < liEven.length; i++) {
   liEven[i].style.background = 'pink';
}

console.log(items);
```

## Moving Around the DOM
```js
// Moving around the DOM

let val;

const list = document.querySelector('ul.collection');
const listItem = document.querySelector('li.collection-item');

val = listItem;
val = list;

// Get Child nodes
val = list.childNodes; // returns a NodeList
// This isn't really what we want though, as it reutrns back CRLF as their own node. This isn't ideal as it would need to be filtered further.

// Get children element nodes
val = list.children; // HTMLCollection with only the elements
val = list.children[0].nodeType; // Returns the type of item, see following list
// 1 - Element
// 2 - Attribute (deprecated)
// 3 - Text node
// 8 - Comment
// 9 - Document itself
// 10 - Doctype

val = list.children[1];
list.children[1].textContent = 'Hello';

// Children of Children
val = list.children[3].children;

// firstChild
val = list.firstChild; // Will give the first child item, not just elements
val = list.firstElementChild; // Will reutrn only the first element

// lastChild
val = list.lastChild;
val = list.lastElementChild;

// childElementCount - count the number of child elements
val = list.childElementCount;

// get parent node
val = listItem.parentNode;
val = listItem.parentElement;

// get parents parent
val = listItem.parentElement.parentElement; // can chain multiple times

// get next sibling
val = listItem.nextSibling; // deals with all items, not just elements
val = listItem.nextElementSibling; // only looks at elements
val = listItem.nextElementSibling.nextElementSibling;

// get previous sibling
val = listItem.previousSibling; // deals with all items, not just elements
val = listItem.previousElementSibling; // only looks at elements

console.log(val);
```

💚