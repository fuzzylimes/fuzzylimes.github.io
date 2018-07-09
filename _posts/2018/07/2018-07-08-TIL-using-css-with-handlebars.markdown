---
layout: post
title:  "TIL: Using css with handlebars"
date:   2018-07-08 20:35:00 -0000
categories: TIL
---
In order to import a css file into a handlebars project in nodejs, there's one small thing that's required to be done before the file will be accessible from the template files.

First, you'll need to include the `path` module:
```js
const path = require('path');
```

Second, you'll need to create a new public folder in the project. Then create another folder, `css`, inside that folder.

Third, you'll need to make that public folder accessible by the project:
```js
app.use(express.static(path.join(__dirname, '/public')));
```

Finally within your main handlebars template, you can now import css files from this folder:
```html
<link rel="stylesheet" href="/css/bootstrap.min.css">
```

💚