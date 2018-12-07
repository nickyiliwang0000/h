Advanced JS: Lexical Scope & Execution Context

### How JavaScript is compiled

Our JavaScript files are not directly read by the browser. There's a step in between our writing and the browser's interpretation where the JS code is compiled (i.e. translated from something that is human readable to something that the computer can understand).

### The Global Object

When the browser first loads a script, that script is run inside of a `global execution context`. (Execution context: the environment that a function executes in.) Initially, this gives you access to two things: 

    1. The Global Object
    2. The keyword (variable) `this`

Create an empty JavaScript file and run it in the browser. Open the console and type in `this`. What is `this` equal to? 
The `window` object !
This `window` object is the global object when running code in the browser. (It'll be something else if you are running the Javascript on a server). 

When you think of the term `global` in JavaScript, think *code that is not inside a function*. 

### Function Context

Whenever a function is called, a new context is created. Inside the function, there is a private scope where anything declared inside of the function cannot be accessed from the outside. This new execution context also *has reference to it's outer environment.* (This can also be referred to as the *lexical environment*.) 

### Revisiting `this`

The `this` keyword can be one of the most confusing to grasp. Now we know that every time an execution context is created / a function is run, it gives us access to a variable called `this` which can be very useful for writing dynamic code. 

`this` will be pointing at a different object depending on how the function is invoked. Let's look at a few scenarios that change the value of this depending on how the function is called. 

```js
// global scope, we already have access to this
console.log(this); // >> Window

// function declaration in the global scope
function functionDeclaration(){
    console.log(this);
}
//function invocation, execution context is created
functionDeclaration(); // >> Window 

// function expression in the global scope 
let functionExpression = function(){
    console.log(this);
}

functionExpression(); // >> Window
``` 

Whenever a function is declared or a function expression is written in the global scope, `this` will point to the global object even though the execution context has changed. 

Let's take a look at methods inside of objects. 

```js

//object literal is created 
let instructor = {
    name: 'Tiff',
    print: function(){
        console.log(this);
    }
}

// print method is called
instructor.print(); // >> {name: "Tiff", print: f(){}}

```

In this case, since the function is a method (i.e. it is attached to an object), the `this` keyword has the value of the object that contains the method.

Now, let's create a function inside of a method. 

```js
 let instructor = {
      name: 'Tiff',
      print: function(){
          console.log(this);

          let changeName = function(newname){
              this.name = newname;
          }

          changeName('Sylvia');

          console.log(this);
      }
  }

  instructor.print(); // >> {name:'Tiff'} >> {name: 'Tiff'}

``` 

That's confusing! Inside of our `print` method, `this` is a reference to the object it's defined inside of, so it might make sense that our `changeName` function inside that method would also make reference to the same object. This is not the case! Even though it's nested inside your object, it is not *called* on the object, so it's execution context is the global scope. `this` is once again referencing the window object, so this code is actually creating a new global `name` variable and setting it to `Sylvia` (check it out in the console!)

How can this be solved? One way is with ES6 arrow functions! 

### Arrow Functions Revisited

Arrow functions handle the `this` keyword a little differently. They are *lexically scoped*, meaning that they create a *lexical this*, which is a fancy way of saying `this` will always refer to the parent scope. Unlike other types of functions, arrow functions do not have their _own_ `this`. 

Let's rewrite our `instructor` method using an arrow function.

```js
  let instructor = {
      name: 'Tiff',
      print: function(){
          console.log(this);

          let changeName = (newname) => {
              this.name = newname;
          }

          changeName('Sylvia');

          console.log(this);
      }
  }

  instructor.print(); // >> {name:'Tiff'} >> {name: 'Sylvia'}

```

It now works like we want it to! How is that the case? Now that we are using an arrow function for our `changeName` method, it does not have it's own `this` — it uses the `this` from it's enclosing execution context, which is the `print` method. 

Take note that this is a great solution to our nested function problem but could yield some more unexpected results if used in other contexts. 


```js
let cto = {
	name: "Ryan",
	sayName: () => {
		return this.name;
	}
}
console.log( cto.sayName() );
```

In this example, if we changed the function on the `sayName` property from an anonymous function to an arrow function it will not work properly! The `this` will be bound lexically, and in this case it will be the `window` object. 

To learn more about arrow function check out this <a href="https://youtu.be/oTRujqZYhrU?list=PL57atfCFqj2h5fpdZD-doGEIs0NZxeJTX" target="_blank">video</a>!

Understanding what `this` is going to be at any given moment is tricky and comes with a combination of practice and experience. Remember that the easiest way to determine what `this` is set to, is to pop in a `console.log(this)`!

### Syntax Review 

As we start digging in to React, we're going to see a lot more of ES6 arrow functions. 

Remember that this:
```javascript
// standard JavaScript function
let add = function(a,b) {
  return a + b;
}
```

does the exact same thing as this:

```javascript
const add = (a,b) => {
  return a + b;
}
```

which does the exact same thing as this:

```javascript
const add = (a,b) => a + b;
```

Even though the word `return` isn't written in the last example, it is implied. Try to become familiar with this last syntax, because it's going to come up a lot in React!

**Exercise:**

[Arrow Functions Exercises](https://hychalknotes.s3.amazonaws.com/arrow_functions_exercises.zip)