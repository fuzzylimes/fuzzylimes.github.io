---
layout: post
title:  "TIL: Starting with React, Part 3"
date:   2018-06-20 20:25:00 -0000
categories:
  - Coding
tags:
  - react
---
Today's lectures introduced how to deal with conditional operators when working with React. The author of the lectures introduced two different ways to use them when rendering things conditionally based on a specific state. While both of the examples were pretty straight forward, the syntax and handling of it all just seems... I don't know, kind of clunky I guess. Maybe this will be addressed as I go on in the corse, but I can see files getting huge with all of these conditional rendering blocks of code.

Anyways, here are the notes that I collected from this evening's lessons (tomorrow will be handling lists, so I'm eager to jump into that):

## Basic Conditionals
* Can use ternary operator to deal with conditional statements
* For example, you can write an if block in the following way:
```jsx
{ 
    this.state.showPersons ? 
        <div>
            <Person 
                name={this.state.persons[0].name} 
                age={this.state.persons[0].age}/>
            <Person 
                name={this.state.persons[1].name} 
                age={this.state.persons[1].age}
                click={this.switchNameHandler.bind(this, 'fuzzylimes')}
                changed={this.nameChangedHandler}>Hobbies: Cooking</Person>
            <Person 
                name={this.state.persons[2].name} 
                age={this.state.persons[2].age}/>
        </div> : null
}
```
* Could also use something like `this.state.showPersons === true ?...`
* The prefered alternative to this is to do it in a more javascript way, with writing a function within the render method. This will cause the function to be executed/evaluated every time that React needs to re-render the DOM.
```jsx
let persons = null;
if (this.state.showPersons) {
    persons = (
    <div>
        <Person
        name={this.state.persons[0].name}
        age={this.state.persons[0].age} />
        <Person
        name={this.state.persons[1].name}
        age={this.state.persons[1].age}
        click={this.switchNameHandler.bind(this, 'fuzzylimes')}
        changed={this.nameChangedHandler}>Hobbies: Cooking</Person>
        <Person
        name={this.state.persons[2].name}
        age={this.state.persons[2].age} />
    </div>
    );
}
```
* Using this syntax, you only need to include a `{persons}` in the render return.
* This method is recommended over the previous

💚