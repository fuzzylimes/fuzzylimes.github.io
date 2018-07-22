---
layout: post
title:  "TIL: Using Key Values in Express Handlebars"
date:   2018-05-24 20:40:00 -0000
categories:
  - Coding
tags:
  - node.js
---
Today I ran into a situation where I wanted to actually print the key of a key value pair instead of just printing out the value itself. To do this, we can take advantage of the `@key` parameter.

Note that this only works when you have an object of size one. If the object is larger than a size of one, only the first item will be used.

Suppose you pass in the following object into your template: `{"list":[{"apples": 3}]`, and you want to be able to dynamically print that key, whatever it may be. You could do the following in your template:

```html
<div>
{% raw %}
    {{#each list}}
    <table>
        <tr>
            <td>
                {{@key}}
            </td>
            <td>
                {{this}}
            </td>
        </tr>
    </table>
    {{/each}}
{% endraw %}
<div>
```

💚