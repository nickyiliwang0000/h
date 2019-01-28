<!-- Student takeaway: -->
<!-- At the end of this lesson, the student will be able to:

-->
# Lexical scope and execution context
<!-- ## How JavaScript is compiled

Our JavaScript files are not directly read by the browser. There's a step in between our writing and the browser's interpretation where the JS code is compiled (i.e. translated from something that is human readable to something that the computer can understand). -->

## The global object

When the browser first loads a script, that script is run inside of the _global execution context_. An _execution context_ is the environment in which a function is run. _Global_ here means the browser (i.e. code that is **not confined to a function block**). When the browser loads any script (even an empty one), you get access to two things: 

1. The global object
2. The keyword `this`

Create an HTML file and link it to an empty JavaScript file. Open the HTML file in the browser. Open the console and type `this`. What is `this` equal to? 

> The `Window` object !

The `Window` object is the execution context for code in the browser unless otherwise specified.
<!-- (it'll be something else if you are running the JavaScript on a server.) -->
## Specifying execution context

Whenever a function is called, a new context is created. Inside the function, there is a private scope where anything declared inside of the function cannot be accessed from the outside (e.g. variables, functions, etc.). The newly created execution context has can access both to the private scope **and** its outer environment.( This can also be referred to as the **lexical environment.**) 


Lexical scope is another word for static scoping (in other languages)
 -  the opposite of dynamic scope.
Dyna: scope of a variable can change depending on the order of functions called (Lisp -  less common)
Lex: the scope of a variable can be determined from reading the source code.

What is lexical scope?
    Refers to the strategy a programming languages uses to determine where and how veraibles are accessible
What is execution context?
    It's the set of variables that are available to be accessed at any given point as a program is being run.

## Revisiting `this`

The `this` keyword can be challenging to grasp. We know that every time an execution context is created (i.e. a function is run), we have access to a variable called `this` which can be very useful for writing dynamic code. 

`this` will be pointing to a different object depending on how the function is invoked. Let's look at a few scenarios that change the value of `this` depending on how the function is called. 

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

//arrow function in the global scope
let arrowFunction =()=>{
    console.log(this)
}
arrowFunction(); // >> Window

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

### Arrow functions revisited

Arrow functions handle the `this` keyword a little differently. They are )_lexically scoped_, meaning that they create a _lexical `this`_, which is a fancy way of saying `this` will always refer to the parent scope. Unlike other types of functions, **arrow functions do not have their own** `this`. 

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