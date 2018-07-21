---
layout: post
title:  "TIL: Destructuring JS Objects"
date:   2018-07-21 10:32:00 -0000
categories: TIL
---
Today I sat down to focus on better understanding how to destructure javascript objects to make my code a little bit easier to read/manage. Before this morning, I thought that this technique could only be used with flat lists or objects, not with anything nested. But of course, there's a way to do it.

### Object destructuring
First we'll take a look at destructuring objects. The basic idea here is that we'll be using the keys of the object to correlate back to the makes of the variables that we want to define within our block of code.

For this section, we'll be using the following object for each of the examples:
```js
const myHouse = {
    door: 'blue',
    roof: 'black',
    siding: 'tan',
    inside: {
        walls: 'white',
        ceiling: 'white',
        bedroom: {
            location: 'upstairs'
        }
    }
}
```
At the most basic level, we can destructure any of the values on the top level (`door`, `roof`, and `siding`), by using the most basic format (I think I covered that yesterday...):
```js
const { roof } = myHouse; 
console.log(roof); // black
```
That will create a new constant named `roof` which will be equal to the value of `myHouse.roof`, or `black`.

If we want to go a second layer, say to get `inside.walls`, we can do the following:
```js
const { inside: {walls} } = myHouse; // note that inside does not get saved to variable, only walls
console.log(walls); // white
```
This will create a new constant `walls` (note that `inside is NOT created`) which will be equal to `inside.walls` or `white`.

We can take this as many levels deep as we want to (though it does start to get crazy), so here's going one level deeper again:
```js
const { inside: { bedroom: { location } } } = myHouse;
console.log(location); // upstairs
```

Now, what if the object doesn't have these parameters? Well, you're going to be throwing an uncaught exception because the parameter doesn't exist. One way to handle this is to set default values for the parameters you're trying to deconstruct.

If you don't care about setting a specific value, and are cool with your program just not breaking, you can use the following approach of just setting it equal to an empty object:
```js
// Handling default values, using an object
const { inside: { bathroom: { color } = {} } } = myHouse;
console.log(color); // undefined
```
In this scenairo, `color` is going to be set to `undefined`, which can then be handled in your code without blowing things up.

However, if you want to actually give the parameter a default value, there's a little bit more you'd have to do, as you have to handle all of the objects below the specific parameter you care about:
```js
// Handling default values, with a value: version 1
const { outside: { garage: { size = 'small' } = {} } = {} } = myHouse;
console.log(size); // small

// Handling default values, with a value: version 2
const { outside: { garage: { size2 } } = { garage: { size2: 'small' } } } = myHouse;
console.log(size2); // small
```
Both of the above methods will work exactly the same, one is just a bit cleaner than the other.

### Deconstructing arrays
To me, this doesn't seem nearly as useful as deconstructing objects with keys, but it is available if needed.

In this case, since it's an array, everything is related to the order that values appear in the array. So you better know what you have in what order, or you'll just be putting things into random variables.

The basic prinicple is pretty much the same as with objects:
```js
const fruits = ['Apple', 'Pear', 'Grapes'];
const [first, second, third] = fruits;
console.log(third, first, second); //Grapes Apple Pear
```

You can also use `spread` if you want to grab out an array within an array:
```js
const [first1, ...last2] = fruits;
console.log(first1, last2); //Apple [ 'Pear', 'Grapes' ]
```

And that's all good, but that's just single level. What about multi-dimensional arrays?

It starts to get tricky:
```js
// Nested arrays
const numbers = [[0,1,2], [3,4,5], [[6],[7],[8]]];

const [a1, , a3] = numbers;
console.log(a3); // [ [ 6 ], [ 7 ], [ 8 ] ]

const [b1, , [[b3], , ]] = numbers;
console.log(b3); // 6
```
In the first example, you can see that I basically set all three arrays to their own variables (`a1, a2, a3`). In the next step, I take that another level deeper and grab out a specific value from within one of those arrays.

You basically end up building back out the exact array that you're comparing against. That's to say, you better know EXACTLY what you're working with.

💚