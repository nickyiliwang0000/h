<!-- Student takeaway -->
<!-- By the end of this lesson, the student should know:
- What execution context & scope means
- How the `this` keyword works
-->

# Advanced JavaScript: lexical scope & execution context

## Load, compile, & execute

Our JavaScript files are not directly read & run by the browser. The browser's JavaScript engine (the part of the browser dedicated to reading and running JavaScript code) has a step in between loading a script and running it (or executing) called _compilation_. In the compilation step the human-readable script is translated to something that the computer can understand. A few different things happen during the compilation stage that can affect how your code is run. In particular, this is where _execution contexts_ and _scopes_ are determined.

## Execution contexts & scope
During the compilation step, the JavaScript engine scans the code it's been asked to execute and creates an inventory of all the variables and functions each line of code will have access to when it's being run. This inventory is called the _execution context_.

The set of available variables and functions is referred to as the _scope_. JavaScript is said to have a _lexical_ scope strategy because where a variable or function is declared explicitly determines it's availability to the rest of the program.

### The global execution context
When a JavaScript engine first starts with a new script it creates a default execution context called the _Global Execution Context_, which will be available to every level of the script. By default the global execution context gives you access to two things: 

1. The _global object_
2. The `this` keyword

Let's explore what these things are. Create an HTML file and link it to an empty JavaScript file. Open the HTML file in the browser. Open the console and type `this`. What is `this` equal to?

The `Window` object! This object is the global object for any scripts executed in a browser. 

When you think of the term _global_ in JavaScript, think **code that is not inside a function**. 

### Global execution context example
<table><tr><th>
good-grandchild.js
</th><th>
Global Execution Context
</th></tr><tr><td><pre lang="js">
let name = 'Verna';
let age = '72';
function callGrandma() {
  let phoneNumber = '416-555-4321'; 
  phoneCall(phoneNumber, name);
}
callGrandma();
</pre></td><td>

| Item | Inventory |
| ---- | --------- |
| Variables | `name`, `age` |
| Functions | `callGrandma` |
| Other Scopes | _none_ |
| `this` | Reference to `window` |

</td></tr></table>

### Function context

Whenever a function is called, a new execution context is created. All of the variables and functions declared **inside** this function are protected from being accessed or modified by the rest of the script. This is referred to as the "private scope" of the function. This function's execution context also **has a reference to it's outer execution context**. 

### Function execution context example
<table><tr><th>
good-grandchild.js
</th><th>
`callGrandma`'s Execution Context
</th></tr><tr><td><pre lang="js">
let name = 'Verna';
let age = '72';
function callGrandma() {
  let phoneNumber = '416-555-4321'; 
  phoneCall(phoneNumber, name);
}
callGrandma();
</pre></td><td>

| Item | Inventory |
| ---- | --------- |
| Variables | `phoneNumber` |
| Functions | _none_ |
| Other Scopes | `Global Execution Context` |
| `this` | Reference to `window` |

</td></tr></table>

## Revisiting `this`

The `this` keyword is a complex topic that can take some time to master. Every time an execution context is created it gives us access to a variable called `this` which can be very useful for writing dynamic code. 

`this` will be pointing at (or referencing) a different object depending on how the function is defined and called in the script. 

In the following examples, `this` always references the `Window` object:

### `this` in the global execution context
```javascript
console.log(this); 
// >> Window
```

### ...in a declared function's private scope
```javascript
// a function declared in the global scope
function someDeclaredFunction(){
    console.log(this);
}

someDeclaredFunction(); 
// >> Window 
```

### ...in a function expression's private scope
```javascript
let someFunctionExpression = function(){
    console.log(this);
}

someFunctionExpression(); 
// >> Window
``` 

Whenever a function is declared or a function expression is written in the global scope, `this` will point to the global object even though the execution context has changed. 

### Object methods
Let's take a look at `this` inside object methods. 

```javascript
// object literal is created 
let character = {
  name: 'Kermit',
  print: function(){
    console.log(this);
  }
}

character.print(); 
// >> {name: 'Kermit', print: f(){}}
```

In this case, since the function is a method (i.e. it is attached to an object), the `this` keyword references the object that contains the method.

Now, let's create a function inside of a method. 

```javascript
let character = {
  name: 'Kermit',
  print: function(){
    console.log(this);
    let changeName = function(newName){
      this.name = newName;
    }

    changeName('Miss Piggy');
    console.log(this);
  }
}
  
character.print(); 
// >> {name: 'Kermit', ...} 
// >> {name: 'Kermit', ...}

``` 

Why didn't the name change? Inside of our `print` method, `this` references the object in which the print method is defined, so it might seem to make sense that our `changeName` function inside that method would also make reference to the same object. This is not the case! Even though it's nested inside your object, it is not *called* as a property of an object, so the `this` keyword defaults back to the global object, `window`.  This function is actually creating a new global `name` variable and setting it to `"Miss Piggy"` (check it out in the console!)

How can this be solved? One way is with ES6 arrow functions! 

## Arrow functions revisited

Arrow functions handle the `this` keyword a little differently. Unlike the above examples where the means in which a function is called determines one of many different possible values for `this`, arrow functions never have their own `this` value. They always inherit the `this` value from the scope in which the function was defined.  

Let's rewrite our `character` method using an arrow function.

```javascript
let character = {
  name: 'Kermit',
  print: function(){
    console.log(this);
    let changeName = (newName) => {
      this.name = newName;
    }
    
    changeName('Miss Piggy');
    
    console.log(this);
  }
}

character.print(); 
// >> {name: 'Kermit', ...} 
// >> {name: 'Miss Piggy', ...}
```

It now works like we want it to! How is that the case? Now that we are using an arrow function for our `changeName` method, it does not have it's own `this` — it uses the `this` from it's enclosing execution context, which is the `print` method. 

Take note that this is a great solution to our nested function problem but can yield some unexpected results when used in other contexts:

```js
let singer = {
  name: "Beyoncé",
  sayMyName: () => {
    return this.name;
  }
}
console.log(singer.sayMyName());
// >> 
```

In this example, the arrow function assigned to the `sayMyName` property get's it's `this` value from the scope in which the function is defined. The arrow function is defined as part of creating the object in the global execution context, so `this` will reference the global execution context's `this` value, the `window` object.  

To learn more about arrow function check out this <a href="https://youtu.be/oTRujqZYhrU?list=PL57atfCFqj2h5fpdZD-doGEIs0NZxeJTX" target="_blank">video</a>!

Understanding what `this` is going to be at any given moment is tricky and comes with a combination of practice and experience. Remember that the easiest way to determine what `this` is set to, is to pop in a `console.log(this)`!

### Syntax review 

As we start digging in to React, we're going to see a lot more of ES6 arrow functions. 

These examples all do _the same thing_.

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
In addition to the _block body_ style above, arrow functions can also be defined in _consise body_ style. The following is, again, exactly the same as the above:

```javascript
const add = (a,b) => a + b;
``` 

When only an expression is provided to the right of the arrow, the function's `return` value is implied to be that expression. Try to become familiar with this shorthand syntax, because it's going to come up a lot in React!

## Exercise
[Arrow Functions Exercises](https://hychalknotes.s3.amazonaws.com/arrow_functions_exercises.zip)
