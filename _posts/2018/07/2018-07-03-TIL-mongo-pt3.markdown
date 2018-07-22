---
layout: post
title:  "TIL: Back to Learning Mongo, pt3"
date:   2018-07-03 21:45:00 -0000
categories:
  - Coding
tags:
  - mongodb
  - node.js
---
Today concluded the basic mongo operations section with mongoose portion of the course I'm working on. Today basically covered all of the various ways that a record can be updated, either using the instance itself or using the model to make the changes.

Unlike the last few days, I'll keep today's blog more focused (also my notes are getting too long to just keep dumping them here every day).

## Updating Records
* Like delete, there are two different sets of updates
* Model Class specific:
    * `update()`
    * `findOneAndUpdate()`
    * `findByIdAndUpdate()`
* Model Instance specific:
    * `update()`
    * `set and save`
* using `set()` will only update the record in memory NOT in the database. It must be used with `save()` to update the record.
* `save()` is best suited when multiple updates are being done (like having multiple functions that do updates and saving at the end)
* When using `update()` for class, you provide both the query and the replacement:
```js
User.update({name: 'Joe'}, {name: 'Alex'})
```
* All three of the class specific updates work exactly the same (query, replacement)


💚