---
layout: post
title:  "TIL: Back to Learning Mongo, pt4"
date:   2018-07-04 19:45:00 -0000
categories:
  - Coding
tags:
  - mongodb
  - node.js
---
The "mongo" lessons continue. I use quotes because this course has become everything but mongo. On the plus side I'm feeling pretty confident about using promises, async/await, and mocha now!

Today mostly dealt with the concept of subdocuments and virtual types. Subdocuments allows you to embed other documents within documents so that you can have some kind of data relationship within your non-relational database. Virtual Types basically let you write functions to dynamically generate values for properties not stored in mongo.

### Subdocuments
* You can create relation by making subdocuments within a document (for whatever reason)
* Create a new schema for whatever you want, and then embed it into the main model
    * subobjects are not models
* Please use the `findOneAndUpdate()` when adding or removing documents instead of constantly saving every two second.
    * They can be used in conjunction with the `$pull` and `$push` update operators to remove or add records

### Virtual Types
* Used in model, but don't get stored over in mongo
* Whenever the virtual property is refered to, it will call a function back in the model
* This is done by tagging with a getter
```js
UserSchema.virtual('postCount').get(function() {
    return this.posts.length;
});
```
* Notice above how we're using the `this` to access what's calling this function

### Ignoring Mocha Tests
You can skip a mocha test by chaning the `it` to a `xit`. That will cause the test not to be executed.

### Switching Windows of Same Type on Mac
I've owned my mac for almost 2 years at this point, and I just now learned this today. Since `cmd + tab` only cycles through your apps, you actually have to use `cmd + ~` key to cycle between open windows for an app. Would have been nice to know a year or so ago...

💚