---
layout: post
title:  "TIL: Back to Learning Mongo, pt6"
date:   2018-07-06 20:55:00 -0000
categories: TIL
---
Today's lessons were pretty bad. Very frustrated with the class that I've been taking. Reached the halfway point where I'm ready to just drop it as I don't feel like it's really providing me anymore. Feel like I'm still having to google for answers on basic things WITHIN the course itself.

Case in point, today I we covered sorting. But the sorting we covered only dealth with assuming that all records start with a capitalized letter. But what happens if you have a mix of cases on your key?

Well, turns out that sort is case sensitive. Meaning that if you have users `[Al, andy, Bob]`, the records would be returned as `[Al, Bob, andy]` when sorted.

The way to fix this is to use the `coallation` method to tell mongo how to treat all of the strings it's using to key off of. So this ends up looking something like this:
```js
it('can skip and limit the result set', (done) => {
    User.find({})
        .collation({locale: 'en'})
        .sort({name: 1})
        .skip(1)
        .limit(2)
        .then((users) => {
            console.log(users);
            assert(users.length == 2);
            assert(users[0].name == 'Joe');
            assert(users[1].name == 'Maria');
            done();
        });
});
```

Using the list form before, this will put things in the expected order of `[andy, Al, Bob]`.

💚