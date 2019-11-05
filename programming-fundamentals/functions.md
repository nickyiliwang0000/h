<!-- Student takeaway: -->
<!--Student will be able to:
- Know that there are 3 ways to define a function (declaration, expression, arrow)
- Know the difference between an argument and a parameter
- Know the difference between return and console.log()
- Write a function of their own with parameters using each syntax
-->
# Functions

[We said before](https://github.com/HackerYou/bootcamp-notes/blob/master/programming-fundamentals/intro-to-javascript.md#debugging-tools) that functions are chunks of code that can be run at any point in time. Functions are arguably the most important and powerful concept in any programming language, but this is especially true for JavaScript. 
<!-- where, as we'll see, functions can be passed around like any other value. -->

So far we've mostly worked with built-in functions; now it's time to learn how to create your own.

The purpose of writing a function is to reduce verbosity in your code. Why write a set of instructions multiple times when you can create a function to do the work for you? Repeat less code!

## Defining a function

A function is _defined_ by giving it a name and the code you would like it to execute, and then _called_ by referencing the name at a later point in the code. To define a function, we use the `function` keyword followed by the name of the function. The syntax looks like this:

```js
function nameOfFunction() {
  // block of statements to execute
}
```

**Example**:

```js
function helloWorld() {
  console.log("Hello there!");
}
```
This syntax for defining a function is called a [function declaration](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function). There are other ways to define function. For example, like this:

```js
const helloWorld = function() {
  console.log("Hello there");
};
```
This second method of defining a function is referred to as a [function expression](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/function). Using one or the other is usually a matter of personal preference, and for our purposes at this point they are exactly the same. 

## Calling a function
We call the function by typing its name followed by smooth brackets. Note that your function will never run if you don't call it!

```js
const helloWorld = function() {
  console.log("Hello there");
};

helloWorld();
// "Hello there!"
```

**Exercise:** Write a function called `sayMyName` that will `alert` your name, then call the function.

## Parameters

Functions can do much more than execute the exact same code over and over. This is where _parameters_ come in. Parameters are the comma-separated list of variables that serve as placeholders for the values we can pass to the function (i.e. the _arguments_).

Parameters are the placeholders, arguments are the actual values that get passed into a function.

```js
function nameOfFunction(parameter1, parameter2) {
  // block of statements to execute
}
```
Here is the same thing, but defined as a function expression:
```js
const nameOfFunction = function(parameter1, parameter2) {
  // block of statements to execute
};
```

Using parameters, you can change what a function that will return:

**Example**:

```js
const add = function(a, b) {
  return a + b;
}

const result = add(2, 4);

console.log(result); // 6
```

1. Here we **define** a function called `add` that takes the parameters `a` and `b` and returns their sum. 
2. Then we declare a variable in which we **call** the function and **pass** it the **values** `2` and `4` as **arguments**. 
    * Inside the function, `a` refers to the value `2` and `b` refers to the value `4`. 
3. The variable `result` stores the **return** of the function - the value `6` - which we then console log.

**Exercise:** Edit your `sayMyName` function to accept one parameter called `name`, then call it. It should alert the name that was passed in as an argument. 

## `return` vs. `console.log()`

Our functions will generally do one of two things: 
1. return a value
1. print (i.e.log) some information to the console

They are not the same. Logging a value to the console using `console.log()` does not make that value available for reuse within our code.  To do that, we must use the `return` keyword.

The following function prints a value to the console:

```js
const addition = function(a, b) {
  console.log(a + b);
}
```

If we try to store the result of the function we see that our variable stored nothing; the value is `undefined`.

```js
const num = addition(1, 2);
num; //undefined
```

If we use a `return` statement, we can make the function a lot more useful.

```js
const adding = function(a, b) {
  return a + b;
}
```

```js
const number = adding(1, 2);
number; //3
```
## Arrow functions
Arrow functions are a newer syntax for creating functions (created in ES6). Arrow functions are not going to replace the function declarations and expressions we know and love, but we will be seeing them more and more. This is the basic arrow function syntax:

```js
const functionName = (parameter1, parameter2) => {
  //some code
};
```

The core part of the syntax is the lack of the `function` keyword. Instead, we have the `=>` or _fat arrow_. Even within this syntax, there are a few different ways to define the arrow function.

For example, if the function only returns a value and there is nothing else in the function body, we can remove the `{}` around it, make it one line and remove the `return` keyword:

<table>
<tr>
  <th>shorthand</th>
  <th>...is the same as</th>
  <th>...is also the same as</th>
</tr>
<tr>
<td>
<pre lang="js">
const add = (a,b) => a + b;
</pre>
</td>
<td>
<pre lang="js">
const add = (a,b) => {
  return a + b;
};
</pre>
</td>
<td>
<pre lang="js">
const add = function(a,b) {
  return a + b;
};
</pre>
</td>
</tr>
</table>

If the function only has one parameter you can  leave the `()` off as well:

<table>
<tr>
  <th>shorthand</th>
  <th>...is the same as</th>
  <th>...is also the same as</th>
</tr>
<tr>
<td>
<pre lang="js">
const addFive = a => a + 5;
</pre>
</td>
<td>
<pre lang="js">
const addFive = (a) => {
  return a + 5;
};
</pre>
</td>
<td>
<pre lang="js">
const addFive = function(a) {
  return a + 5;
};
</pre>
</td>
</tr>
</table>

However, if there are no parameters, you **must** include the smooth brackets:

<table>
<tr>
  <th>shorthand</th>
  <th>...is the same as</th>
  <th>...is also the same as</th>
</tr>
<tr>
<td>
<pre lang="js">
const eight = () => 3 + 5;
</pre>
</td>
<td>
<pre lang="js">
const eight = () => {
  return 3 + 5;
};
</pre>
</td>
<td>
<pre lang="js">
const eight = function() {
  return 3 + 5;
};
</pre>
</td>
</tr>
</table>

**Exercise**: How can we use the `add()` function to add three numbers together without changing the definition of the function?

```js
const add = function(a, b) {
  return a + b;
}
```
> Remember that this function returns a value whose data type is number.

<!-- Expected answer:
Pass the function as an argument:  add(add(1,2), 3).
-->

## Terminology recap
Term | Definition
---|---
Define | to create a function
Parameter | a variable (placeholder) for the arguments when defining a function
Argument | a value provided to a function
Pass | to provide arguments to a function
Call | to ask JavaScript to evaluate a function Return| to pass back a value from a function

## Intro to scope

In JavaScript, *scope* defines the visibility or accessibility of our variables.

When working with functions, the parameters and variables that we define _inside_ of a function are visible and accessible only within that function and are not accessible outside of the function. This is known as *function scope* (sometimes referred to as *local scope*).

Any variables defined outside of a function have *global scope*. This means that these variables can be accessed anywhere within an application, including within functions.

```js
// global scope

const myFirstFunction = function(){
  // function (local) scope
}

// global scope

const mySecondFunction = function(){
  // function (local) scope
}

// global scope
```

Knowing the different scope levels helps us to better insulate our code from bugs. We don’t need to know too much more about scope at this stage as we will be exploring it in-depth in a later lesson.


## Exercises
Complete the functions exercises in [functions.html](https://hychalknotes.s3.amazonaws.com/functions.html).

The solutions are available [here](https://hychalknotes.s3.amazonaws.com/functions-ANSWER.html).
