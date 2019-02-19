<!-- Student takeaway: -->
<!-- At the end of this lesson, the student will be able to:

-->
# Lexical scope and execution context

<!-- ## The JavaScript engine
The path between the JavaScript code we write and what we see in our browser is not an unbroken line. There's a step in between our writing and the browser's interpretation where the code is compiled by the JavaScript engine in the browser (i.e. translated from something that is human-readable to something that the computer can understand). The way your functions and variables are interpreted depends on how the engine reads your file. It's not necessary to completely understand this lesson to be able to use JavaScript effectively, but learning these concepts is a pathway to a deeper understanding of JavaScript. They're the "why", rather than the "how". -->

## Execution context

_Execution context_ refers to the environment in which a function is run. The browser's JavaScript engine creates execution contexts while your code is running. There are three types of execution contexts in JavaScript but we'll only be talking about two: _global_ and _functional_.
<!-- The third type is eval. -->

> An excellent description of context comes from [this blog post](http://ryanmorr.com/understanding-scope-and-context-in-javascript/): JavaScript is a single threaded language, meaning only one task can be executed at a time. When the JavaScript interpreter initially executes code, it first enters into a global execution context by default. Each invocation of a function from this point on will result in the creation of a new execution context.

So, _functional execution context_ is created every time a function is called. _Global execution context_ is the default context for the whole page.

> You can think of functional execution context as a snapshot of the program when a function is called and global execution context as a series of continuously updating snapshots.

When the browser loads any script (even an empty one), a global execution context is created, which means you get access to two things: 

1. The global object
2. The keyword `this`

Create an HTML file and link it to an empty JavaScript file. Open the HTML file in the browser. Open the console and type `this`. What is `this` equal to? 

> The `Window` object !

Right now, the global object and `this` are the same thing. That's because a global execution context has been created inside the window. 
<!-- (it'll be something else if you are running the JavaScript on a server.) -->

## Specifying `this`
Whenever a function is called, a new functional context is created. That functional context assigns a value to `this`.

> In other literature you might see `this` referred to as "context" - a bit of a linguistic challenge. Think of `this` as part of an execution context in the same way the word "context" is part of the phrase "execution context".

The value of `this` changes depending on **how** the function is called.
If it's called as method on an object, `this` will refer to the parent object:

```js
const myObject = {
    myMethod: function() {
        console.log(this);   
    }
};
// logs the object called myObject
```
What if a method is nested inside the object?
```js
const myObject = {
    myMethod: function() {
        console.log(this); 
        let myNestedFunction = function(){
            console.log(this)
        }
    }
};
// logs the object called myObject 
// logs
```

If a function is called just plain in a JavaScript file, `this` is the window object:
```js
const myFunction = function(){
    console.log(this)
}
myFunction();
```
> Remember? The global execution context!

<!-- If a function is created using a `new` constructor, `this` depends on where the new instance of the function was created; it will usually be the parent. -->

Inside the function, there is a private scope where anything declared inside of the function cannot be accessed from the outside (e.g. variables, other functions, etc.). The newly created execution context is the lexical scope of a function, because it contains both the information      (which is lexical in scope) describes what is true about both to function's private scope **and** its outer environment. 

<!-- (This can also be referred to as the **lexical environment.**)  -->

<!-- 
Lexical scope is another word for static scoping (in other languages)
 -  the opposite of dynamic scope.
Dyna: scope of a variable can change depending on the order of functions called (Lisp -  less common)
Lex: the scope of a variable can be determined from reading the source code.

What is lexical scope?
    Refers to the strategy a programming languages uses to determine where and how veraibles are accessible
What is execution context?
    It's the set of variables that are available to be accessed at any given point as a program is being run. -->


## Scope
So, we already know that when a variable is declared inside of a function, it's inaccessible outside of that function.

## Revisiting `this`

We mentioned that the `this` keyword will refer to an object when used in a method. And now we know that every time an execution context is created (i.e. a function is run), we have access to a `this`. 

The value of the `this` variable is assigned when the function is created and can be reassigned depending on how the function is called.

Let's look at a few scenarios that change the value of `this`:

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