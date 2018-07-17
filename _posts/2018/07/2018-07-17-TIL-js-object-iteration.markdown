---
layout: post
title:  "TIL: Javascript Object Iteration"
date:   2018-07-17 18:10:00 -0000
categories: TIL
---
I came across an interesting article this morning that talked about various ways in which to handle iterating over object in javascript. Both of these methods were foreign to me and it turned out to be a great read.

[Here's a link to the article I'll be talking about](https://dmitripavlutin.com/how-to-iterate-easily-over-object-properties-in-javascript/). It looks like the author has a lot of very informative blog posts like this one.

In the blog, Dmitri talks about two diffent techniques of iterating over objects: using `Object.values()` and `Object.entries()`. Both of these were new to me, I've pretty much only ever used `Object.keys()` before (and boy did I use it a lot in the `ute` probject I'm just now wrapping up).

### `Object.values()`
So `Object.values()` on its own will basically grab all of the values out of the object (assuming object is flat) and stick them into an array object. For example:
```js
> a = { a: 'apple', b: 'dog'}
{ a: 'apple', b: 'dog' }
> Object.values(a);
[ 'apple', 'dog' ]
```

Once you've got that array set up, you can use a `for ... of` to loop over the data, like so:
```js
for (let b of Object.values(a)){
    console.log(b);
}
// apple, dog
```

### `Object.entries()`
On its own, `Object.entries()` is going to create an array of arrays, where both the key and the value get placed into an array. Re-using the example before:
```js
> Object.entries(a);
[ [ 'a', 'apple' ], [ 'b', 'dog' ] ]
```

We can then use a `for ... of` to loop over these values:
```js
for(let [letter, thing] of Object.entries(a)){
    console.log(`${letter} - ${thing}`);
}
// a - apple, b - dog
```

But perhaps more interesting that this is that this format sets up perfectly to be turned into a Map (something that I honestly have never worked with outside of maybe one tutorial):
```js
> let mappings = new Map(Object.entries(a));
> mappings
Map { 'a' => 'apple', 'b' => 'dog' }
> mappings.get('a');
'apple'
```

💚