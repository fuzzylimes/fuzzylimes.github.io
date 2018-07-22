---
layout: post
title:  "TIL: Javascript Basics: Part 3"
date:   2018-05-08 18:10:00 -0000
categories:
  - Coding
tags:
  - javascript
---
Not much time to spend on things today, but I did make it through a few more lessons. More basic Javascript items today.

## Date and Times
```js
let val;
const today = new Date(); // Current date/time
let birthday = new Date('9-10-1981 11:25:00');
birthday = new Date('September 10 1981');
birthday = new Date('9/10/1981');

val = today;
console.log(typeof val); // Date
val = birthday; // 

val = today.getMonth(); // numerical representation of month
val = today.getDate(); // numerical representation of date
val = today.getDay(); // numerical representation of day of week
val = today.getFullYear(); // year
val = today.getHours(); // hours
val = today.getMinutes(); // minute of hour
val = today.getSeconds(); // seconds of hour
val = today.getMilliseconds(); // milliseconds of hour
val = today.getTime(); // epoch time

birthday.setMonth(2); // March 10th
birthday.setDate(12); // March 12th
birthday.setFullYear(1985); // March 12th 1985
birthday.setHours(3);
birthday.setMinutes(30);
birthday.setSeconds(25);

console.log(val);
```

## If Statemenets and comparison operators
```js
const id = 100;

// Equal to
if(id == 100){
    console.log('CORRECT');
} else {
    console.log('INCORRECT');
}

// Not Equal to
if(id != 101){
    console.log('CORRECT');
} else {
    console.log('INCORRECT');
}

// equal to value & type
if(id === '100'){
    console.log('CORRECT');
} else {
    console.log('INCORRECT');
}

// not equal to value & type
if(id !== '100'){
    console.log('CORRECT');
} else {
    console.log('INCORRECT');
}

// Test if undefined
if(typeof id !== undefined){
    console.log(`The ID is ${id}`);
} else {
    console.log('NO ID');
}

// Greater or less than
if(id > 200){
    console.log('CORRECT');
} else {
    console.log('INCORRECT');
}

// if else
const color = 'red';

if(color === 'red'){
    console.log('Color is red');
} else if(color === 'blue'){
    console.log('Color is blue');
} else {
    console.log('Color is not red or blue');
}

// Logical Operators
const name = 'Steve';
const age = 20;

// And &&
if(age > 0 && age < 12) {
    console.log(`${name} is a child`);
} else if(age >= && age <= 19){
    console.log(`${name} is a teenager`);
} else {
    console.log(`${name} is an adult`);
}

// Or ||
if(age < 16 || age > 65){
    console.log(`${name} can not run in race`);
} else {
    console.log(`${name} is registered for the race`);
}

// Ternary operator
console.log(id === 100 ? 'Correct': 'Incorrect');

// without braces
if(id === 100)
  console.log('Correct');
else
  console.log('Incorrect');
```

💚