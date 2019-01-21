# Debugging JavaScript

## Comments
Sometimes you want to write notes to yourself (or others) to organize blocks of code or leave explanations. Just like HTML & CSS, JavaScript will ignore comments and not execute them.

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

Multi-line comments are also great for "hiding" large blocks of code so you can try something new without erasing your old code.

**Get used to commenting your code.** Comments help you (or other developer)understand your code in the future.

## Debugging tools

_Functions_ are chunks of code that do something. Functions can be repeated as many times as you want. We can create our own functions (to be discussed later) but there are many handy ones already built into JavaScript for debugging purposes. 

### Function basics
To get the function to execute, you have to **call the function** using the function name followed by parentheses:
```js
functionName();
```

Some times this is also referred to as **running** or **executing** a function.

Sometimes you will need to _pass_ some data into the function. This data is called an _argument_.

```js
functionName(argument);
```

You can pass more than one piece of data to a function by using a comma:
```js
functionName(firstArgument, secondArgument);
```

Terminology reminder:
* **Argument:** a value provided to a function
* **Pass:** to provide arguments to a function
* **Call:** ask JavaScript to evaluate/execute a function
* **Return:** pass back the value from the function

### Debugging functions
A few built-in JavaScript functions that we will use are `prompt()`, `alert()` and `confirm()`. All three display a dialog box containing a message. `prompt()` also allows the user to input some text. `confirm()` also includes 'Cancel' and 'OK' buttons.

These dialogs are built into the browser and not generally able to be restyled for use in production code but they are useful debugging tools.

Let's try calling these functions in the browser console with and without arguments and see what happens, one function at a time.

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
* if the user clicks the 'Cancel' button, the function returns `null` (i.e. "value of nothing")

#### `alert()`:

* the **argument** shows in the dialog
* returns `undefined` (i.e. "does not have a value")

#### `confirm()`:

* returns `true` if 'OK' was selected
* `false` if "cancel" was selected

Note that the arguments being passed and some of the values being returned were contained within quotes. This is because their data type is `string`. [Here's a refresher on that](https://github.com/HackerYou/bootcamp-notes/blob/917b7a927d55c11314045c6c5a625b3c31ba1a53/programming-fundamentals/intro-to-programming.md).

### console.log()

Likely the debugging tool that you'll be using the most is `console.log()` which is a function you can use any time you want to print (display) something in the console. You can use this any time you are unsure of what the value of a variable is, or when you want to check that one of your functions is working properly! 

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

There should be nothing in the console on a production website.

