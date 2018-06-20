---
layout: post
title:  "TIL: Starting with React, Part 2"
date:   2018-06-19 20:25:00 -0000
categories: TIL
---
More work on my React corse today. Made it through the begining section that covered the rest of the basics and even completed my first react project assignment, ~wooo. Today I'm just going to cover the rest of the notes that I took during the lessons today.

## Handler Functions
* Use the label `Handler` to note handler methods inside of components
* DO NOT use `()` for method calls, just pass reference
* Supported events: https://reactjs.org/docs/events.html#supported-events
* If state or props changes, react will check to see if something would change on DOM, and update to reflect those changes.
    * These are the only two things that can be used to cause an update on the page
* State should only be updated in select components (containers). The rest of the smaller components should NOT change the state.

## Method References between Components
* You can pass in a method of one component to another using props
* Can use `bind` to pass in a parameter to a method
* Can also use a function call to do the update
    * Can affect perfomance, bind is recommended.


💚