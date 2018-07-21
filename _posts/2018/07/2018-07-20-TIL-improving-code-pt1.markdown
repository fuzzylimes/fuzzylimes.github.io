---
layout: post
title:  "TIL: Impoving My JS Code, pt1"
date:   2018-07-20 19:30:00 -0000
categories: TIL
---
As I posted yesterday, I want to start spending some time focusing on making my code a bit cleaner so that it's a bit better from the start. So today I'm starting to go back through the best practicies document I posted yesterday and start implementing some of what they outline

### Using computed property names when creating dynamic object properties
This is honestly something that I've wanted to know for a loooong time. I guess in theory it might be forwned upon because you don't know what's being created for sure, but man... does it make things nice.

Essentially what this allows you to do so create a property in an object with a key set equal to that of one of your variables.

To see what I mean, lets look at this example:
```js
function getKey(k) {
    const names = {
        0: "Al",
        1: "Bob",
        2: "George"
    }
    return names[k];
}

const obj = {
    id: 5,
    name: 'San Francisco',
    [getKey(1)]: true,
};

console.log(obj);
```
Ignoring the fact that this opens yourself up to a can of different problems, lets look at what it actually does do. A name will be returned by the `getKey()` function based on the int that's passed in. That name that is returned is then set as the key by wrapping it in the brackets `[]`. Super neat

### Defining methods in objects
When defining a method in an object, it's best to use a short hand method definition. That is, rather than setting a key equal to a function, simply just define the function right inside the object itself:
```js
const atom = {
    value: 1,

    doubleValue() {
        return atom.value*2;
    },

    addValue(value=9) {
        return atom.value + value;
    },
}

console.log(atom.addValue(5));
console.log(atom.addValue());
console.log(atom.doubleValue());
atom.value = 5;
console.log(atom.addValue());
```

### Use property value shortcuts
This is a neat trick that I always forget to use. If you want to assign a property to a variable with the same name as the value, you can simply just put the variable name:
```js
const purpleHaze = 'Purple Haze';
const obj2 = {
    purpleHaze,
};
console.log(obj2);
```

### Don't call `Object.prototype` methods directly
Rather than calling `obj.hasOwnProperty(val)`, it's recommended to actually cache the lookup within the module for faster usage. This makes it clear what's actually being evaluated, and avoids issues that might come if trying to run the method on something like an empty object:
```js
const has = Object.prototype.hasOwnProperty;
const obj3 = "Dog";
console.log(has.call(obj2, 'purpleHaze')); // true
console.log(has.call(obj3, 'purpleHaze')); // false
```

### Use the object spreader when making shallow copies
This is only when making shallow copies, but it's recommended to use the spread operator. This can also be used to omit items that you don't care about:
```js
const original = { a: 1, b: 2 };
const copy = { ...original, c: 3 };
const { a, ...noA } = copy;
console.log(copy);
console.log(noA);
```

💚