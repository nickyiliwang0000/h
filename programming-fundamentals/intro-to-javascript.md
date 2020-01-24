<!-- Student takeaway: -->
<!--Student will know:
- That JavaScript was created quickly
- That a REPL is a place to test out code
- What pseudo code is and to write it in the comments
- The data types we will be working with (SNUBON(S))
- The difference between an expression and a value
- How to use prompt(), alert(), and confirm()
- What each of those built-in functions returns
 -->

# Intro to JavaScript
## JavaScript
The first iteration of the language that we know as JavaScript was developed over 10 days in 1995. Its purpose was to allow developers to add functionality and interactivity to the browser, something that was not possible at the time. You'll hear lots of people complain about JavaScript's faults, but for something that was created in a bit over a week, it's pretty impressive!

JavaScript's working draft name was _Mocha_ and its first name when it went live in the Netscape Navigator browser was _LiveScript_. Colloquially it's known as JavaScript, but it's official name is actually _ECMAScript_; it is overseen and maintained by the European Computer Manufacturers' Association. (This isn't suuuuper important, but when you see the initialism `ES6`, you'll know that it stands for ECMAScript, spec 6, which is JavaScript!)

### TL;DR
```js
JavaScript === ECMAScript
```

#### More about JavaScript
* [A re-introduction to JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript) (just the Introduction for now)
* [JavaScript Overview](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/JavaScript_Overview)

## REPL

_REPL_ stands for read, evaluate, print, loop. A _REPL enviroment_ is an interactive environment in which you can type instructions for the computer. The computer will read, evaluate/run, and print the results of those instructions. Then the computer then makes itself ready for the next instruction (i.e. loops).

A JavaScript REPL is available in the dev tools of your browser. Open the JavaScript REPL by navigating to the 'Console' tab.

Your console will look slightly different depending on your browser, but there should be an angle bracket `>` or two `>>` with an input beside it. The cursor should start blinking when you click into the input. Give the computer a simple instruction like `1 + 1`, press enter. The REPL will return a value!

```js
> 1 + 1
// 2
```

Cool, right?! This is a great environment you can use to test out your fledgling JavaScript skills.

## Expressions and values
A _value_ is a piece of data (more abstractly, a sequence of 0's and 1's).

An _expression_ is any piece of code or instruction given to the computer that produces a value.

```js
//this is an expression
> 1 + 1
// this is the value produced by that expression
2
```
In the console, the value is returned immediately after you press enter.

Vocabulary is very important in JavaScript because it helps us ask coherent questions and adds structure to our thinking. Just as we learned **selector**, **rule**, **property** and **value** in CSS, so we will drill **expression** and **value** into your head now.

## Data types

Every JavaScript value has a _type_ which can determine where that value can be used. Here are some types you will encounter:

Data type | Description | Example
---|---|---
number | Integers & decimals/floats | `10`, `10.001`
string | Characters including spaces | `'internetUser993'` `"123 Main St."`
boolean | A reserved keyword that looks like an English word | `true`, `false`
undefined | Does not have a value | `undefined`
null | Has a value of nothing | `null`
object | A set of organized data | `{studentNumber:231, instructor:"Hyram Outke"}`

> There's also an ES6 data type called Symbol but it's used mostly in library creation and you won't see it much in this course.

If you want a mnemonic, some of our instructors like **SNUBON(S)**.

### typeof

There is a special operator we can use to check types called `typeof`. When used with a value it will tell us the type of that value. 

```js
typeof "Juno College";
//string

typeof 3792
//number

typeof "a bunch of fibers rolled up together";
//string

```
There are some gotcha-y cases for `typeof`, but for now we'll be using it with things we expect to be numbers, strings, or booleans.

## Comments
Sometimes you want to write notes to yourself (or others) to organize blocks of code or leave explanations. JavaScript will ignore comments as long as they're flagged correctly.

Single line comments can be added with `//`.

```js
// There are 365 days in a year.
```

Just like in CSS, `/*  */` are used for multiline comments.

```js
/* 
  Many 
  Lines!
  ....Wow
*/
```

Multiline comments are also great for hiding large blocks of code so you can try something new without erasing your old code. Remember to remove them at production, though!

## Pseudo code
When you're writing JavaScript (or other code) it can be helpful to map the detailed steps your program will carry out in plain English, just like we did in the alien exercise. This is called _pseudo code_ and it's a useful strategy for organizing your ideas about how a program should run without worrying about the language's syntax. It's like outlining an essay in point form before going back and writing the actual essay.

```json
when the user scrolls down the page:
* measure how far they've scrolled
* if they've scrolled more than 400px
  - show a tooltip
* otherwise
  - hide the tooltip
```

Every project you write should have pseudo code. We will often require it, so get into the habit of writing it now!

## Debugging tools

_Functions_ are chunks of code that do something. Functions can be repeated as many times as you want. We will create our own functions soon but first let's take a look at a couple handy functions built into JavaScript that we can use for debugging. 

### Function basics
To get the function to execute, you have to _call_ it using the function name followed by parentheses:

```js
functionName();
```

Sometimes this is also referred to as _running_ or _executing_ a function.

Sometimes you will need to _pass_ some data into the function. This data is called an _argument_.

```js
functionName(argument);
```

You can pass more than one piece of data to a function by using a comma:
```js
functionName(firstArgument, secondArgument);
```
When you call a function, it does something, and very often it will _return_ a value to you.

<!-- All fuctions in JS technically have a return. Beyond Bootcamp goes into this. -->

Terminology recap:
* An **argument** is a value provided to a function.
* To **pass** is to provide arguments to a function.
* To **call** a function is to ask JavaScript to evaluate/execute a function.
* To **return** is to pass back the value from the function. Often, this value is called "the return".

### Debugging functions
A few built-in JavaScript functions that we will use are `prompt()`, `alert()` and `confirm()`. All three display a dialog box containing a message. `prompt()` also allows the user to input some text. `confirm()` also includes 'Cancel' and 'OK' buttons.

These dialogs are built into the browser and not able to be restyled for use in production code but they are useful when we're working on our projects.

Let's try calling these functions in the browser's console REPL with and without arguments and see what happens, one function at a time.

**Without arguments**
```js
prompt();
alert();	
confirm();
```

**With arguments**  
> Note that the arguments are contained in quotes. Which data type is that?
```js
prompt("What is your name?");
alert("hello");
confirm("yay or nay?");
```

In the example above, the **values** "What's your name?", "hello" and "yay or nay" are **passed** as **arguments** to the functions named `prompt` and `alert`. We **called** the function and it **returned** different values for each function.

#### `prompt()`
* when the user clicks 'OK', the text entered in the input field is returned
* if the user clicks 'OK' without entering any text, an empty string is returned
* if the user clicks the 'Cancel' button, the function returns `null` (i.e. a value of nothing)

#### `alert()`:

* the **argument** shows in the dialog
* no matter what, this function returns `undefined` (i.e. "does not have a value") because the function doesn't produce a value.


#### `confirm()`:

* returns `true` if 'OK' was selected
* `false` if 'Cancel' was selected

Note that the arguments being passed and some of the values being returned were contained within quotes. This is because their data type is `string`.

### console.log()

Likely the debugging tool that you'll be using the most is `console.log()` which is a function you can use any time you want to print (i.e. display) something in the console. You can use this any time you are unsure of what the value of a variable is, or when you want to check that one of your functions is working properly! 

```js
// log out a string
console.log('oh joy of joys my event listener is firing');

// log out a variable
console.log(myVar);

// log out multiple variables 
console.log(raphael, donatello, michelangelo, leonardo);

// evaluate expressions
console.log(total*tax);
```

Whenever you want to check the status of something in your code, use `console.log`! Use them liberally in development and **remove console logs from your projects when they are ready for deployment**.

## There should be nothing in the console on a production website.