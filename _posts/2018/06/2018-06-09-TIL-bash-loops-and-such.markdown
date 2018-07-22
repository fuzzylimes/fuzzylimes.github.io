---
layout: post
title:  "TIL: Looping in bash scripts and other things"
date:   2018-06-09 19:30:00 -0000
categories:
  - Coding
tags:
  - bash
---
I was in need of writing some bash scripts today to handle the automation of some of my test runs. in the past, most of my "bash scripting" was limited to putting a command into a file and ending it with `.sh`. Today I branched out a bit more and dealt with looping, command line arguments, and other fun stuff.

### Arguments in bash
Args are pretty simple in bash scripts. Whatever you put in will be read as a string and assigned to a variable equal to the number of their position. For instance, if I were to run the script below using the command `./myscript.sh hello 123 butts`: 

```sh
echo "$3 $2 $1 $0"
```

Then it would echo back out `butts 123 hello myscript.sh`

### Looping in bash
For loops are supported in bash scripts, pretty similar to how they work in python. It follows the `for <var> in <something>` format. That something could be an array or list of items or numbers. For instance:

```sh
for i in {1..20}
do
echo "$i"
done
```

will echo back the numbers 1 - 20 on a seperate line.

### Passing in numbers
Because the script interperts all of the command line arguments as strings, I had to find a way to get numbers to be converted back to numbers. I wanted to be able to define the number of times an action would be looped by providing it as an argument.

The easy way of doing this is to perform a math operation on the value. That forces bash to treat the variable as an int. So to do so, you can use the format:

```sh
a=$(($1+0))
echo "$a"
```

This will convert your variable into an int. That could then be fed into your loop:

```sh
a=$(($1+0))
for i in $(seq 1 $a)
do
echo "$i"
done
```

Note that we switch to using a sequence here, with basically does the samething as the number array.

### Setting an array of strings
Arrays are created in `()` brackets with a single space separating items. No commas used.

```sh
a=( "string1" "string2" "string3" )
```

💚