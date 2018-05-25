---
layout: post
title:  "TIL: Express Query Strings and Handlebar Arrays"
date:   2018-05-24 20:40:00 -0000
categories: TIL
---
I got a chance to work on my side project a little more at work today (though to be fair it's hardly a side project as it's going to be used to do actual work), and things are really starting to come together. One of the big things that I got working today involved handling query strings with express.

## Express and Query Strings
Express makes handling query strings super easy. Lets suppose you have the following route configured in your app:

```js
app.get('/testing', (req, res) => {
    res.setHeader('Content-Type', 'application/json');
    res.send({ id: 1234 });
});
```

If you were to access the `/testing` route on the server, you'd get back the json payload with `{"id": 1234}`. Now, if you wanted to be able to support some type of query string on this route like `/testing?bananas=3`, you would be able to use `res.query` to get your query parameters in object form. The previous banana example would return the following:

```json
{"bananas": 3}
```

The same logic applies if you have more that one parameter. Say we expand out this example with `/testing?bananas=3&apples=4&grapes=1`. You'd see the following object in `res.query`:

```json
{"bananas": 3, "apples": 4, "grapes": 1}
```

## Express Handlebars and Arrays
Something else I remembered that I learned today that took a bit of searching to find an answer/example for. When using `express-handlebars` and you're passing in an array to your template, if you want to iterate over this array and use the value, you use the `{{#each}}` tag along with a `{{this}}` tag to actually use the value.

For instance, suppose that I have an array of four numbers: `[12, 34, 45, 221]`. Passing them into my html template, I would do the following to iterate through them:

```handlebars
<div>
    {{#each list}}
    <ul>{{this}}</ul>
    {{/each}}
<div>
```
That would give you an unordered list of the four numbers you passed in.

💚