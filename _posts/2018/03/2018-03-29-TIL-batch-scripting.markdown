---
layout: post
title:  "TIL: Batch scripting"
date:   2018-03-29 17:00:00 -0500
categories: TIL
---
Starting back up the blogs with what I had intended to use them for in the first place: Today I Learned notes. This first entry in the series will be covering my first experience with batch scripting.

Here we go.

# Batch Scripting
I have a confession to make: in all of the years of working in Window's shops I'd actually never written a batch script before today. I knew that they could be written, but I'd just never had an instance where I needed to write one.

Well, that all changed today.


## My Problem
We needed to migrate our mongoDB related test activities off from using a Linux box to using Windows instead (we use a Windows only automation framework at work). After getting mongoDB installed for windows, I was pleased to see that the mongo --exec command was working like I was used to it working back on Linux.

The problme was with running these commands. Because of the way that the automation tool is written, there's not a way to do variable replacement within the command that would need to be sent to the command line (...don't get me started).

So the thought was: create a batch script that would take the values I needed in as arguements, and then plug them into the command. EZPZ

## What I learned
### 1. Passing in command line parameters
Command line parameters can be passed in just like they could in shell scripts. Every thing included after the file name can be passed into the file. For example, if you've just got basic things to pass in, like words or numbers, it's as easy as this:

`myawesomescript.batch variable1 variable2`

BUT (of course there's a but), I needed to do something a little more facy. Specifically I needed to pass in a list of values. To get around this, I found you could simpy wrap the array in double quotes and it could be read in:

`myawesomescript.batch "['variable', 'variable2']"`

Great!

### 2. Storing the parameters
In order to use the parameters, batch scripts use the `%` sign with a number. So to access the first variable, you'd use `%1`. To access the second, `%2`, etc.

To make them easier to work with, they can be saved off to variables using the `SET` command:

```Batch
SET arg1=%1
SET arg2=%2
```
This was fine for basic parameters, but wasn't good enoungh for handling passing in string lists. Because the list had to be quoted to be read in, there are now leading characters around the list that needs to be added into my command.

To strip off the leading and trialing characters, you can do somthing silly like this:

```Batch
SET arg1="['a','b']"
SET mod1=%arg1:~1,1%
```
This will scrip off the leading and trailing character, leaving you with just `['a','b']`.

### 3. Building the command.
With all of the variables passed in, all I needed to do was build my command. In order to use the saved variables, you wrap the variable with `%` signs:

```Batch
ECHO Today is %day%
```
