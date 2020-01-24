<!-- Student takeaway -->
<!-- By the end of this lesson, the student should:
- Know what execution context and scope are
- Know how the `this` keyword works
- Have more experience with arrow functions
-->

# Advanced JavaScript: lexical scope and execution context

## Load, compile, and execute

Our JavaScript files are not directly read and run by the browser. The browser's _JavaScript engine_ (the part of the browser dedicated to reading and running JavaScript code) has a step in between loading and running (or _executing_) a script called _compilation_. In the compilation step, the human-readable script is translated to something that the computer can understand. A few different things happen during the compilation stage that can affect how your code is run. In particular, this is where _execution contexts_ and _scopes_ are determined.

## Execution contexts and scope
During the compilation step, the JavaScript engine scans the code it's been asked to execute and creates an inventory of all the variables and functions each line of code will have access to when it's being run. This inventory is called an _execution context_.

The set of available variables and functions is referred to as the _scope_. JavaScript is said to have a _lexical_ scope strategy because **where** a variable or function is declared explicitly in the code determines its availability to the rest of the program.

### The global execution context
When a JavaScript engine first starts a new script, it creates a default execution context called the _global execution context_, which will be available to every level of the script. By default the global execution context gives you access to two things: 

1. The _global object_
2. The `this` keyword

Let's explore what these things are. Create an HTML file and link it to an empty JavaScript file. Open the HTML file in the browser. Open the console and type `this`. What is `this` equal to?

> The `window` object! The `window` object is the global object for any scripts executed in a browser. 

When you think of the term _global_ in JavaScript, think **code that is not inside a function**. 

### Global execution context example
<!-- NOTE: The weird function indentation in the example below is needed for github to render the code properly --> 
<table><tr><th>
good-grandchild.js
</th><th>
Global execution context
</th></tr><tr><td><pre lang="js">
let name = "Verna";
let age = "72";

    function phoneCall(number, person){
      console.log("Calling " + number + "for " + person)
    }
  
    function callGrandma() {
      let phoneNumber = "416-555-4321"; 
      phoneCall(phoneNumber, name);
    }
callGrandma();
</pre></td><td>

| Item | Inventory |
| ---- | --------- |
| Variables | `name`, `age` |
| Functions | `callGrandma`, `phoneCall`|
| Other scopes | _none_ |
| `this` | Reference to `window` |

</td></tr></table>

### Function context

Whenever a function is **called**, a new execution context is created. All of the variables and functions declared **inside** this function are protected from being accessed or modified by the rest of the script. This is referred to as the _private scope_ of the function. A function's execution context also **has a reference to it's outer execution context**. 

**Example of function context**

<!-- NOTE: The weird function indentation in the example below is needed for github to render the code properly --> 
<table><tr><th>
good-grandchild.js
</th>
<th>
<strong>callGrandma</strong>'s execution context
</th>
</tr>

<tr><td><pre lang="js">
let name = "Verna";
let age = "72";

    function phoneCall(number, person){
      console.log("Calling " + number + "for " + person)
    }

    function callGrandma() {
      let phoneNumber = "416-555-4321"; 
      phoneCall(phoneNumber, name);
    }
callGrandma();
</pre></td><td>

| Item | Inventory |
| ---- | --------- |
| Variables | `phoneNumber` |
| Functions | _none_ |
| Other scopes | `global execution context` |
| `this` | Reference to `window` |

</td></tr></table>

## Revisiting `this`

The `this` keyword can take some practice to master. Every time an execution context is created it assigns a value to a variable called `this` which can be very useful for writing dynamic code. 

Depending on how a function is defined or called, its `this` keyword will point at (or _reference_) a different object.

In the following examples, `this` always references the `window` object:

### `this` in the global execution context
```javascript
console.log(this); 
// >> Window
```

### `this` in a declared function's private scope
```javascript
// a function declared in the global scope
function someDeclaredFunction(){
    console.log(this);
}

someDeclaredFunction(); 
// >> Window 
```

### `this` in a function expression's private scope
```javascript
const someFunctionExpression = function(){
    console.log(this);
}

someFunctionExpression(); 
// >> Window
``` 

Whenever a function is declared or a function expression is written in the global scope, `this` will point to the global object **even though** the execution context has changed. 

### Object methods
Let's take a look at `this` inside object methods. 

```javascript
// object literal is created 
let character = {
  firstName: 'Kermit',
  introduction: function(){
    console.log(this);
    return `Hello! My name is ${this.firstName}.`;
  }
}

console.log(character.introduction()); 
// >> Object { firstName: "Kermit", introduction: introduction() }
// >> Hello! My name is Kermit.
```

In this case, since the function is a method (i.e. it is attached to an object), and the method is called as a property 
of the object, the `this` keyword references **the object that contains the method**.

Pay attention to that second condition: "the method is called as a property of the object". This condition is a big part
of what makes it challenging to predict what `this` will reference. 

For example, if we create a variable and assign it the object's `introduction` method and then call that variable as a 
function, the `this` keyword will reference a different value. 

```javascript
let character = {
  firstName: 'Kermit',
  introduction: function(){
    console.log(this);
    return `Hello! My name is ${this.firstName}.`;
  }
}

let intro = character.introduction; 
console.log(intro());
// >> Window 
// >> "Hello! My name is undefined."
``` 

When calling **the reference** to `character`'s `introduction` method, the `this` keyword references the global object 
once again. 

This can become problematic organizing your code using objects and then passing those organized methods as callbacks to 
other functions. When the callbacks functions are executed, their `this` value won't reference the organizing object 
any longer. 

```javascript
let character = {
  firstName: 'Kermit',
  introduction: function(){
    console.log(this);
    return `Hello! My name is ${this.firstName}.`;
  }
};

let app = {
  startUp: function(afterStartUpCallback) {
    // Do some start up stuff ...
    
    // Call the provided callback and return whatever it returns
    return afterStartUpCallback() 
  }
};

result = app.startUp(character.introduction);
console.log(result);
// >> Window 
// >> "Hello! My name is undefined."
``` 

Remember that what `this` references is determined by the execution context, **not the scope**. 

A similar situation will occur if you create a function **inside an object method**. Variables in the object method's 
scope will be available to that inner function, but the function's `this` value will be **different** than the 
containing method's `this` value.
  
```javascript
let fourSidedDie = {
  numbers: [1,2,3,4],
  roll: function() {
    console.log(this); 
    // Object { numbers: [] ... } if called as `fourSidedDie.roll()`, `Window` otherwise 
  
    let possibleNumbers = this.numbers;
    function newRandomNumber() {
      // the code here can't access fourSidedDie's properties or methods because 
      // the newRandomNumber function cannot be called **as a property on 
      // the fourSidedDie object**. But it CAN access the variables in scope from 
      // the parent function.

      console.log(this); // Window
      console.log(this.numbers); // undefined 
      console.log(possibleNumbers); // [1,2,3,4]
  
      return possibleNumbers[Math.floor(Math.random() * possibleNumbers.length)];
    }
        
    return newRandomNumber();
  }
}

fourSidedDie.roll();
```

How can we make what `this` references more predictable? One way is with arrow functions! 

## Arrow functions revisited

Arrow functions handle the `this` keyword a little differently. Unlike the above examples where the way a function is called determines one of many different possible values for `this`, arrow functions **never** have their own `this` value. They **always** inherit their `this` value from the scope in which the function was defined.  

Let's rewrite our `newRandomNumber` method using an arrow function.

```javascript
let fourSidedDie = {
  numbers: [1,2,3,4],
  roll: function() {
    console.log(this); // Object { numbers: [] ... } if called as `fourSidedDie.roll()`, `Window` otherwise 
  
    let newRandomNumber = () => {
      // the code here can't access dice's properties or methods because the newRandomNumber function cannot be called 
      // *as a property on the dice object*. But it CAN access the variables in scope from the parent function.

      console.log(this); // Object { numbers: [] ... }
      console.log(this.numbers); // [1,2,3,4]
  
      return this.numbers[Math.floor(Math.random() * this.numbers.length)];
    }
        
    return newRandomNumber();
  }
}

fourSidedDie.roll();
```

It now works like we want it to! How is that the case? We are using an arrow function for our `newRandomNumber` method, which means that the `newRandomNumber` function does not have it's own `this`: it uses the `this` from its enclosing execution context, which is the `roll` method. 

Take note that this is a great solution to our nested function problem but can yield some unexpected results when used in other contexts:

```js
let song = {
  artist: "Carly Rae Jepsen",
  title: "Call Me Maybe",
  
  artistAndTitle: () => {
    return `${this.artist} - ${this.title}`;
  }
}
console.log(song.artistAndTitle());
// >> "undefined - undefined"
```

In this example, the arrow function assigned to the `artistAndTitle` property get's it's `this` value from the scope in which the function is defined. The arrow function is defined as part of creating the object in the global execution context, so `this` will reference the global execution context's `this` value, the `window` object.  

To learn more about arrow functions check out this [video](https://youtu.be/oTRujqZYhrU?list=PL57atfCFqj2h5fpdZD-doGEIs0NZxeJTX)!

Understanding what `this` is going to be at any given moment comes with a combination of practice and experience. Remember that the easiest way to determine what `this` is set to is to `console.log(this)`!

### Syntax review 

As we start digging in to React, we're going to see a lot more arrow functions. 

Reminder, these examples all do **the same thing**.

<table><tr><th>
Declarative
</th><th>
Expression
</th><th>
Arrow
</th></tr><tr><td><pre lang="js">
function add(a, b) {
  return a + b;
}
</pre></td><td><pre lang="js">
const add = function(a,b) {
  return a + b;
}
</pre></td><td><pre lang="js">
const add = (a, b) => {
  return a + b;
}
</pre></td></tr></table>

#### Arrow function shorthand syntax
In addition to the _block body_ style above, arrow functions can also be defined in _concise body_ style. The following is, again, exactly the same as the above:

```javascript
const add = (a,b) => a + b;
``` 

When only an expression is provided to the right-side of the arrow, the function's `return` value is implied to be that expression. Try to become familiar with this shorthand syntax, because it's going to come up a lot in React!


<!-- > Q: Are arrow functions and function declarations and function expressions the exact same!?
> A: **No!** But, if the function you're writing does not use `this` or `arguments` and is not called with `new`, they act the same.  -->

## Exercise
Try these [exercises](https://hychalknotes.s3.amazonaws.com/arrow-functions-exercises--bootcamp.zip) to practice writing arrow functions.

## More reading on scope and `this`
* [Scope in JavaScript](http://www.digital-web.com/articles/scope_in_javascript/) -  an easy-to-read explanation of scope with a neighborhood analogy.
* [How does the `this` keyword work?](https://stackoverflow.com/questions/3127429/how-does-the-this-keyword-work) - a great StackOverflow answer with a little quiz!
* [How does a browser read JavaScript?](https://stackoverflow.com/questions/15395347/does-a-browser-truly-read-javascript-line-by-line-or-does-it-make-multiple-passe) -  an answer with many links to lower-level computing concepts.
