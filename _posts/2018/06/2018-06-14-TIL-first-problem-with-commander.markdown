---
layout: post
title:  "TIL: First problem with commander..."
date:   2018-06-14 21:00:00 -0000
categories: TIL
---
In yesterdays blog I talked about how I found out about the node package `commander` for handling command line properties. Well, when I went to start using it in a project today, I ran into the same issue that evidently everyone runs into...

For what seems like at least the last 4 years now, there have been multiple open issues regarding the fact that commander will not make an argument mandatory if that argument has a mandatory field.

Before we get to the why and how, lets look at a simple example of how commander works:

```js
const commander = requires('commander');

commander
  .version('0.0.1')
  .option('-n, --number <num>', 'Number of things')
  .parse(process.argv);

console.log(commander.number);
```

Above I define that I will have one option when using the app, `number` and that it will be accessible either by using `-r` or `--r`. By using the `< >` brackets, I note that a parameter is required when using that flag. Finally, I give a definition of the argument when running `-h` for help.

However, there's no way to actually mark that the `-n` flag is required when using this means of defining your application options. Even though I've denoted that a parameter is required, that only will be enforced when actually setting the `-n` flag in the command line. Runing without the `-n` will bypass any and all checks.

So, the simple solution I found to this was to simply do the following:

```js
const commander = requires('commander');

commander
  .version('0.0.1')
  .option('-n, --number <num>', 'Number of things')
  .parse(process.argv);

if (!commander.number) {
    console.log('-n is mandatory. See help for more details on how to use the flags');
    process.exit(1);
}

console.log(commander.number);
```

This way, we check to see if the required parameter has been set up front. If it hasn't, we abort right away. If it has, we continue on.

💚