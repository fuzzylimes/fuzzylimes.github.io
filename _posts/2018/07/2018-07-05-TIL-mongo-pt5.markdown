---
layout: post
title:  "TIL: Back to Learning Mongo, pt5"
date:   2018-07-05 20:55:00 -0000
categories:
  - Coding
tags:
  - mongodb
  - node.js
---
Really not feeling it today. Like at all.

Went through another section of Mongo training. This one actually talked about a pretty interesting topic of how to handle relationships within mongodb. So this means being able to related documents within different collections to one another. I honestly didn't even know that was a thing.

Today's going to be another note dump day. Forgive me:

## Referencing between collections
* Setting up references between documents between collections (think relational DB)
* Assign an object with type `Schema.Types.ObjectId` and a ref equal to a model name:
```js
const BlogPostSchema = new Schema({
    title: String,
    content: String,
    comments: [{
        type: Schema.Types.ObjectId, 
        ref: 'comment'
    }]
});
```
* This ref value MUST match what's being defined in model, as shown below:
```js
const Comment = mongoose.model('comment', CommentSchema);
```
* Mongoose does magic behind the sceens when associating the data. In the following steps, Mongoose is actually handling the id referencing:
```js
joe = new User({name: 'Joe'});
blogPost = new BlogPost({
    title: 'JS is great',
    content: 'Sure it is'
});
comment = new Comment({
    content: 'This is a comment'
});
joe.blogPosts.push(blogPost);
blogPost.comments.push(comment);
comment.user = joe;
```
* When doing a query, you can add on a `populate` modifier to fill in the data for a specific field:
```js
it.only('saves a relation between a user and a blog post', (done) => {
    User.findOne({ name: 'Joe' })
        .populate('blogPosts')
        .then((user) => {
            console.log(user);
            done();
        });
});
```
* There is no way to recursively crawl like this. You only get one.
    * Mongoose will not allow it
* ... But evidently there is a way to do it? Not sure why it was said that it wasn't possible:
```js
it.only('saves a full relation tree', (done) => {
    User.findOne({name:'Joe'})
        .populate({
            path: 'blogPosts',
            populate: {
                path: 'comments',
                model: 'comment',
                populate: {
                    path: 'user',
                    model: 'user'
                }
            }
        })
        .then((user) => {
            assert(user.name === 'Joe');
            assert(user.blogPosts[0].title === 'JS is great');
            assert(user.blogPosts[0].comments[0].content === 'This is a comment');
            assert(user.blogPosts[0].comments[0].user.name === 'Joe');
            done();
        });
});
```

💚