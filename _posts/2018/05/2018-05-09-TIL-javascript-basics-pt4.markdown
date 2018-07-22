---
layout: post
title:  "TIL: Javascript Basics: Part 4"
date:   2018-05-09 17:20:00 -0000
categories:
  - Coding
tags:
  - javascript
---
Still moving along with JS lessons. More review again today.

## Switches
```js
const color = 'red';

switch(color){
    case 'red':
      console.log('Color is red');
      break;
    case 'blue':
      console.log('Color is blue');
      break;
    default:
      console.log('Color is not red or blue');
      break;
}

let day;
switch(new Date().getDay()){
    case 0:
        day = 'Sunday';
        break
    case 1:
        day = 'Monday';
        break
    case 2:
        day = 'Tuesday';
        break
    case 3:
        day = 'Wednesday';
        break
    case 4:
        day = 'Thursday';
        break
    case 5:
        day = 'Friday';
        break
    case 6:
        day = 'Saturday';
        break
}
console.log(`Today is ${day}`);
```

## Functions expressions and Declarations
```js
// declarations
function greet(){
    //console.log('Hello');
    return 'Hello';
}
console.log(greet());

// pass in arguements
function greet(firstName, lastName){
    //console.log('Hello');
    return 'Hello ' + firstName + ' ' + lastName;
}
console.log(greet('John', 'Doe'));

// default parameters in es5
function greet(firstName, lastName){
    if(typeof firstName === 'undefined'){firstName = 'John'}
    if(typeof lastName === 'undefined'){lastName = 'Doe'}
    return 'Hello ' + firstName + ' ' + lastName;
}
console.log(greet());

// default parameters in es6
function greet(firstName = 'John', lastName = 'Doe'){
    return 'Hello ' + firstName + ' ' + lastName;
}
console.log(greet());

// function expressions - putting a function as a variable assignment
const square = function(x = 3){
    return x*x;
};
console.log(square(8));

// Immidiately invokable function expressions - IIFEs
// Function runs as soon as declared
(function()){
    console.log('IFFE Ran...');
})();

// with parameters
(function(name)){
    console.log('Hello ' + name);
})('Brad');

// Property Methods
const todo = {
    add: function(){
        console.log('Add todo..');
    },
    edit: function(id){
        console.log(`Edit todo ${id}`);
    }
}
todo.delete = function(id){
    console.log(`Delete todo ${id}`);
}
todo.add();
todo.edit(22);
todo.delete(22);
```

## Loops and itterations
### Loops
```js
// For loop
for(let i = 0; i < 10; i++){
    console.log(i);
}

// continue and break
for(let i = 0; i < 10; i++){
    if(i === 2){
        console.log('2 is my favorite number');
        continue; // Goes to next itteration without continuing
    }

    if(i === 5){
        console.log('Stop the loop');
        break; // kills the loop
    }

    console.log('Number ' + i);
}

// While loop
let i = 0;
while(i < 10){
    console.log(`Number ${i}`);
    i++;
}

// Do while - always runs at least once
let i = 0;
do {
    console.log(`Number ${i}`);
    i++;
} while (i < 10 );

// Looping through arrays
const cars = ['Ford', 'Chevy', 'Honda', 'Toyota'];
for(let i = 0; i < cars.length; i++){
    console.log(cars[i]);
}

// forEach array loop
const cars = ['Ford', 'Chevy', 'Honda', 'Toyota'];
cars.forEach(function(car){
    console.log(car);
});

// forEach extra parameters
const cars = ['Ford', 'Chevy', 'Honda', 'Toyota'];
cars.forEach(function(car, index, array){
    console.log(`${index}: ${car}`);
    console.log(array;)
});

// Map - create an array based on specified parameters
const users = [
    {id:1, name: 'John'},
    {id:2, name: 'Sarah'},
    {id:3, name: 'Karen'}
];
const ids = users.map(function(user){
    return user.id;
});
console.log(ids); // [1, 2, 3]

// For in loop (used with objects)
const user = {
    firstName: 'John',
    lastName: 'Doe',
    age: 40
}

for(let x in user){  // will set the key of each value in user to x
    console.log(x);
    console.log(`${x}: ${user[x]}`)
}
```

## Window Methods, Objects, Properties
```js
// Alert
window.alert('hello world');

// Prompt - pop up with text box
const input = prompt();
alert(input);

// Confirm - pop up confirmation box
if(confirm('Are you sure?')){
    console.log('YES');
} else {  // If cancel selected...
    console.log('NO');
}

// Outter height and width
let val;
val = window.outerHeight;
val = window.outerWidth;

// Inner height and width
let val;
val = window.innerHeight;
val = window.innerWidth;

// Scroll points - where the scroll bar is at
let val;
val = window.scrollY;
val = window.scrollX;

// Location Object - page information
let val;
val = window.location;
val = window.location.hostname;
val = window.location.port;
val = window.location.href
val = window.location.search;

// Redirect
window.location.href = 'http://google.com';

// Reload
window.location.reload();

// Hisotry Object
window.history.go(-1); // Goes back to last history by index
val = window.history.length;

// Navigator Object
val = window.navigator;
val = window.navigator.appName;
val = window.navigator.appVersion;
val = window.navigator.userAgent;
val = window.navigator.platform;
val = window.navigator.vendor;
val = window.navigator.language;
```

## Scope
```js
// Global Scope
var a = 1;
let b = 2;
const c = 3;

function test(){
    var a = 4;
    let b = 5;
    const c = 6;
    console.log('Function Scope: ', a, b, c);
}

test();

// Block scope
if(true){
    var a = 4; // global a will be overritten by this line. var is weird, and is always global
    let b = 5;
    const c = 6;
    console.log('Function Scope: ', a, b, c);
}

for(let a = 0; a < 10; a++){
    console.log(`Loop: ${a}`);
}

console.log('Global Scope: ', a, b, c);
```

💚