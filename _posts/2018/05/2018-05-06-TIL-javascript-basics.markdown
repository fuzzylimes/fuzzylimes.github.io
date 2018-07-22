---
layout: post
title:  "TIL: Javascript Basics"
date:   2018-05-06 17:50:00 -0000
categories:
  - Coding
tags:
  - javascript
---
As I mentioned in my post yesterday, I'm pretty over `golang` at this point in time. After spinning my wheels for weeks, I wanted to get back into something that I better understand and have some enjoyment working with. So today I decided to go back to working with javascript and start on a course that actually teaches the base language.

I've completed a few different Node.js projects, but I've never actually formally taken the time to learn the JS language. I've picked up enough over the time working in Node and writing postman scripts that I have a good idea of how to do what I do know, but I know there's a lot that I've never seen before.

So today was a lot of review for me, most of this was stuff that I've known for a while now. Still there were a few new methods thrown in throughout that I hadn't known about, so that's cool.

Here are all the notes from my training today on vanilla JS:

## Basics

#### Notes
* No issue using either single `'` or double `"` quotes, it's all preference/styling

#### Loging to console
```js
console.log('hello world!');
console.log(123);
console.log(true);
var greeting = 'Hello');
console.log(greeting);
console.log([1,2,3,4]);
console.log({a:1, b:2})
console.table({a:1, b:2})

console.error('This is some error')
console.clear();
console.warn('This is a warning');
console.time('Hello'); // Time it takes to reach start to end of section
  console.log('hi');
  console.log('hi');
  console.log('hi');
  console.log('hi');
console.timeEnd('Hello');
```

#### Comments
```js
// Single Line Comment

/*
Multi
Line
Comment
*/

```

#### Defining Variables
* var - basic javascript variable that's been around since the beinging
* const - used to define a constant that cannot be changed
* let - new way of assigning a variable, good for scoping

##### var
```js
var name = 'John Doe';
console.log(name);
name = 'Steve Smith';
console.log(name);

// Init var
var greeting;
console.log(greeting);
greeting = 'Hello';
console.log(greeting);

// Can only contain letters, numbers, _, $
// Can not start with a number
var name = 'John';

// leading with $ usually reserved to working with jquery
// leading with _ usually reserved to private variables
// just be safe and start with a letter

// Multi word vars
var firstName = 'John'; // Camel case, used for most variables
var first_name = 'Sara'; // Underscore
var FirstName = 'Tom'; // Pascal case, usually used with classes and objects
var firstname;
```
##### let
* works identical to `var` on the global level

```js
let name = 'John Doe';
console.log(name);
name = 'Steve Smith';
console.log(name);

let fruit;
```

##### const
* value cannot be reassigned
* can not be initialized as empty (must have value)
* If set to object, values in object can be changed, but not the object itself.

```js
const name = 'John';
// name = 'Sara';

// Cannot init empty
// const greeting;

const person = {
    name: 'John',
    age: 30
}

person.name = 'Sara';
person.set = 'F';
//person = 'Bob';

console.log(person);

const numbers = [1,2,3,4,5];
numbers.push(6);
// numbers = [1,2,3,4,5,6,7];
console.log(numbers);
```

## Data Types
### Background
* Primitive
    * data is stored directly in the location that the variable acesses
    * stored on the statck
* Reference
    * accessed by reference
    * objects that are stored on the heap
    * a pointer to a location in memory

### Primitive Types
* String - strings of characters
* Number - ints, floats, doubles
* Boolean - true/false
* Null - intentionally null
* Undefined - no value (value not assigned)
* Symbols (ES6)

### Reference Types
* Arrays
* Object Literals
* Functions
* Dates
* Anything else

### Examples
#### Primitive
##### String
```js
const name = 'John Doe';
console.log(typeof name);
```

##### Number
```js
const age = 45;
console.log(typeof age);
```

##### Boolean
```js
const hasKids = true;
console.log(typeof hasKids);
```

##### Null
```js
const car = null;
console.log(typeof car); // Incorrectly returns type of Object (early JS bug)
```

##### Undefined
```js
let test;
console.log(typeof test);
```

##### Symbol
```js
const sym = Symbol();
console.log(typeof sym);
```

#### Reference - Objects
##### Array
```js
const hobbies = ['movies', 'music'];
console.log(typeof hobbies);
```

##### Object literal
```js
const address = {
    city: 'Boston',
    state: 'MA'
}
console.log(typeof address);
```

##### Date
```js
const today = new Date();
console.log(typeof today);
```

## Type Conversions
### Number to String
```js
let val;
val = 5;

console.log(val); // 5
console.log(typeof val); // number
console.log(val.length); // undefined - only works on strings!
console.log(String(val)); // Convert number to string

val = string(4+4)
console.log(val); // '8'
console.log(typeof val); // string
```

### Boolean to String
```js
let val
val = String(true);
console.log(val); // 'true'
console.log(typeof val); // string
```

### Date to String
```js
let val
val = String(new Date());
console.log(val); // 'Date'
console.log(typeof val); // string
```

### Array to String
```js
let val
val = String([1,2,3,4]);
console.log(val); // '1,2,3,4'
console.log(typeof val); // string
```

### toString()
```js
let val
val = (5).toString();
val = (true).toString();
```

### String to Number
```js
let val
val = '5';
val = Number(val);
val = Number(true); // 1
val = Number(false); // 0
val = Number(null); // 0
val = Number('hello'); // NaN - Not a number
val = Number([1,2,3]); // NAN

console.log(val.toFixed(2)); // Returns number to two decimal places
```

### parseInt
```js
let val
val = parseInt('100'); // val = 100
val = parseInt('100.34'); // val = 100
```

### parseFloat
```js
let val
val = parseInt('100.34'); // val = 100.34
```

💚