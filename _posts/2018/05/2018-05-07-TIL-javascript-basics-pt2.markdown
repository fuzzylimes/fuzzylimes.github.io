---
layout: post
title:  "TIL: Javascript Basics: Part 2"
date:   2018-05-07 20:30:00 -0000
categories: TIL
---
Still working my way through the basics/fundamentals sections of my JS course. Lots more review today, but I did pick up a few new methods/functions that I didn't know about. Just like yesterday, here are my notes from my session today.

## Numbers/Math
```js
const num1 = 100;
const num2 = 50;
let val;

// simple math with numbers
val = num1 + num2; // 150
val = num1 * num2; // 5000
val = num1 - num2; // 50
val = num1 / num2; // 2
val = num1 % num2; // 0

// math object
val = Math.PI;
val = Math.E;
val = Math.round(2.8); // round to 3
val = Math.round(2.4); // round to 2
val = Math.ceil(2.4); // 3
val = Math.floor(2.8); // 2
val = Math.sqrt(64); // 8
val = Math.abs(-3); // 3
val = Math.pow(8,2); //64
val = Math.min(2,33,45,34,26); // 2
val = Math.max(2,33,45,34,26); // 45
val = Math.random(); // random number 0-1
val = Math.random() * 20; // random number 0-19
val = Math.floor(Math.random() * 20 + 1); // random int 1-20
```

## Strings
```js
const firstName = 'William';
const lastName = 'Johnson';
const age = 30;
const str = 'Hello my name is Brad';
const tags = 'web design,webdevelopment,programming';
let val;

val = firstName + lastName; // WilliamJohnson

// Concat
val = firstName + ' ' + lastName;
// Append
val = 'Brad ';
val += 'Traversy';
val = 'Hello, my name is ' + firstName + ' and I am ' + age;
// Escaping
val = 'That\'s aswesome, I can\'t wait';
// Length
val = firstName.length; // don't need parens, property not method
// concat()
val = firstName.concat(' ', lastName); // William Johnson
// Change case
val = firstname.toUpperCase(); // WILLIAM
val = lastName.toLowerCase(); // johnson
// Get character at position
val = firstName[2];
// indexOf()
val = firstName.indexOf('l'); // 2
val = firstName.lastIndexOf('l'); // 3
// charAt()
val = firstName.charAt('2'); // l
// Get last char
val = firstName.charAt(firstname.length -1); // m
// substring()
val = firstName.substring(0, 4); // Will
// slice()
val = firstname.slice(0,4); // Will
val = firstname.slice(-3); // iam
// split()
val = str.split(' '); // ['Hello', 'my', 'name', 'is', 'Brad']
val = tags.split(','); // ['web design','web development','programming']
// replace()
val = str.replace('Brad', 'Jack');
// includes() - returns bool if item is present in string
val = str.includes('Hello'); // true
val = str.includes('Foo'); // false
```

## Template Literals
```js
const name = 'John';
const age = 31;
const job = 'Web Developer';
const city = 'Miami';
let html;

// Without template strings (es5)
html = '<ul><li>Name: ' + name + '</li><li>Age: '+ age + '</li><li>Job: ' + job + '</li><li>City: ' + city + '</li></ul>';

html = '<ul>' +
       '<li>Name: ' + name + '</li>' +
       '<li>Age: ' + age + '</li>' +
       '<li>Job: ' + job + '</li>' +
       '<li>City: ' + city + '</li>' +
       '</ul>';

// With template strings (es6)
function hello() {
    return 'hello';
}

html = `
  <ul>
    <li>Name: ${name}</li>
    <li>Age: ${age}</li>
    <li>Job: ${job}</li>
    <li>City: ${city}</li>
    <li>${2 + 2}</li>
    <li>${hello()}</li>
    <li>${age > 30 ? 'Over 30' : 'Under 30'}</li>
  </ul>
`;

document.body.innerHtml = html;
```

## Arrays and Array Methods
```js
const numbers = [43, 56, 33, 23, 44, 36, 5];
const number2 = new Array(22, 45, 33, 76, 54);
const fruit = ['Apple', 'Banana', 'Orange', 'Pear'];
const mixed = [22, 'Hello', true, undefined, null, {a:1, b:1}, new Date()]; // can hold any type
let val;

// Get array length
val = numbers.length; // 7
// Check if is array
val = Array.isArray(numbers); // true
val = Array.isArray("string"); // false
// Get single value
val = numbers[3]; // 23
val = numbers[0]; // 43
// Insert into array
numbers[2] = 100;
// Find index of value
val = numbers.indexOf(36); // 5
// Mutating arrays
numbers.push(250); // append to end of array
numbers.unshift(120); // prepend to start of array
numbers.pop(); // pop item from end
numbers.shift(); // remove item from start
// splice()
numbers.splice(1,1); // position to start, and end removal
numbers.splice(1,3); // removes 56, 33, 23
// reverse()
numbers.reverse(); // returns array in reverse order
// Concat array
val = numbers.concat(numbers2); // array with both values in it
// sort()
val = fruit.sort(); // sorted alphabetically
val = numbers.sort(); // sorts by first number, not what you want
// use "compare function"
val = numbers.sort(function(x,y){
    return x - y;
});
// reverse sort
val = numbers.sort(function(x,y){
    return y - x;
});
// find() - takes in a function for searching
function under50(num){
    return num < 50;
}
val = numbers.find(under50); // iterates over items in list, passing value to function. Returns the first that satisfies function.

console.log(numbers);
console.log(val);
```

## Object Literals
```js
const person = {
    firstname: 'Steve',
    lastName: 'Smith',
    Age: 30,
    email: 'steve@aol.com',
    hobbies: ['music', 'sports'],
    address: {
        city: 'Miami',
        state: 'FL'
    },
    getBirthYear: function() {
        return 2017 - this.age; // need to use this to make it local to the object
    }
}
let val;

val = person;
// Get specific value
val = person.firstName; // 'Steve'
val = person['lastName'];
val = person.age; // 30
val = person.hobbies[1]; // sports
val = person.address.state; // FL
val = person['address']['city']; // Miami
val = person.getBirthYear(); // 1987

console.log();

// Array of objects
const people = [
    {name: 'John', age: 30},
    {name: 'Mike'}, age: 23},
    {name: 'Jane'}, age: 32}
];

for(let i = 0; i < people.length; i++){
    console.log(people[i].name);
}
```

💚