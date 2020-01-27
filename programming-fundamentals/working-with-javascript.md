<!-- Student takeaway: -->
<!--Student will be able to:
- Store a function in a variable
- Know that Math. and console.log exist
- Where to insert semicolons (at the end of an instruction but not after a statement block)
- How to link a script file
- How to write script in an HTML file
 -->

# Working with JavaScript

## Combining variables and functions

A variable's value can be set to the return value of a function in JavaScript.

```js
function goodLibraryPatron() {
	return 'library books';
}


let someVariable = goodLibraryPatron();
```
The browser will run the function and store any return from it as the value of the variable.

We know that the `prompt()` function is native JavaScript and allows the user to input text. What if we wanted to hold onto that text to use later?

Using `prompt("What is your name?")`, let's create a variable to hold the value and `alert()` a message with that value.

```js
const name = prompt("What is your name?");
alert("Hello " + name + "!");
// or alert(`Hello ${name}!`)
```

When the browser runs this code, it stops at the `prompt()` function call and waits for the user to input their answer. That returned *value* is then stored into the `name` variable, which we then pass and as an argument to the `alert()` function.

## More built-in functions
We've already looked at `prompt()`, `alert()` and `confirm()` but there are many more functions built into JavaScript. Many of these built-in functions return values that we can store in variables. For example:

* console.log() (doesn't necessarily have a return value)
* `Math.` (always has a return value)
Type `Math.` in the console (without hitting enter) and you'll see a list pop up of available math related functions. E.g., `Math.cos()`, `Math.max()`, `Math.min()` and many more.

Note that these functions look a little different from the ones we previously discussed since they have a `prefix.functionname()` syntax. We will expand on this in [another lesson](https://github.com/HackerYou/bootcamp-notes/blob/master/programming-fundamentals/objects.md).

As with CSS properties, there are too many built-in functions to memorize them all so it's a good idea to have some handy resources nearby. Go to the [MDN](https://developer.mozilla.org/en-US/) and use the search box at the top of the page to learn more about these functions. 

You will need to use these functions for the following exercises:

1. Practice using variables and operators in [variables-operators.html](https://hychalknotes.s3.amazonaws.com/variables-operators.html).
2. After that, give some built in functions a try with [variables-operators-functions.html](https://hychalknotes.s3.amazonaws.com/variables-operators-functions.html).

Answers to both exercises are [here](https://hychalknotes.s3.amazonaws.com/variables-operators-ANSWER.html) and [here](https://hychalknotes.s3.amazonaws.com/variables-operators-functions-ANSWER.html)

## Exploring the DOM

We can access the DOM in _vanilla_ JavaScript with the word `document`. The term vanilla means writing JavaScript without any libraries. 

Let's head to the [Wikipedia page for DOM](https://en.wikipedia.org/wiki/Document_Object_Model) and open up our developer tools.

Type `document` into the console, and notice we get the HTML for the whole page back as a JavaScript object. 

We can access specific parts of the DOM with some built-in JavaScript methods on the `document` object. 

* `document.getElementById('content')` finds an element with the ID of 'content'    

* `document.getElementsByTagName('p')` finds the paragraphs
 
* `document.getElementsByClassName('navbox')` finds all elements with a class of 'navbox'


The Mozilla Developer Network has [documentation](https://developer.mozilla.org/en-US/docs/Web/API/Document) with information about all of the properties and methods of the `document` object.

## JavaScript syntax
Just like any other language, JavaScript has rules that need to be followed in order for you to be understood.

### Semicolons
JavaScript code is composed of statements and expressions that are usually executed one at a time from top to bottom. A semicolon indicates the end of the instruction:

```js
const name = "Your Name";
console.log(name);
	
//same as
	
const name = "Your Name"; console.log(name);
```

> Because of a technique called **automatic semicolon insertion** (ASI), some statements on a new line that are well-formed will be executed as if a semicolon had been added. We encourage you to explicitly add semicolons everywhere they are needed.

```js
// will execute both statements
const name = "Your Name" 
console.log(name);
	
// will throw an error
const name = "Your Name" console.log(name);
```

In the example above, the `console.log(name)` instruction will run as if there was a semicolon after `const name = "Your Name"` thanks to ASI because it is on a new line.

#### Block statements
Single line statements should end in a semicolon but _block statements_ do not. 

Curly brackets, `{ }`, are used to group zero or more statements into what's called a _function block_. 

```js
let singleLineStatement = "one line here"; //needs semicolon
	
if (condition === "something"){
	let singleLineStatement = "one line, that's it!"; //needs semicolon
	let anotherStatement = "one line, a second time!"; //needs semicolon
} //does not need semicolon
```

Here's a handy [Stack Overflow discussion](http://stackoverflow.com/questions/1834642/best-practice-for-semicolon-after-every-function-in-javascript) about when semicolons are needed. And here is a great video  [here](https://www.youtube.com/watch?v=Qlr-FGbhKaI) on the subject.

**Exercise**: In the example below, add the semicolons and line breaks that allow the code to run without errors.

```js
"I'm just a value!" let schoolName = "Juno" let numOfStudents = 40 schoolName + " has " + numOfStudents + " students." 
```

## JavaScript + HTML = ❤️

JavaScript can be added to your HTML pages inline or as an external file, just like CSS.

To include it internally, write all of your JavaScript within a `<script></script>` tag. Though the tags can be added in the `<head>` or anywhere in the `<body>`, it is usually added at the bottom of the page, just before the closing `</body>` tag.

```html
<body>
	<script>
		// js code here
	</script> 
</body>
```

To include it as an external file, save your file using a `.js` extension and link to it using the script tag with a `src` attribute like this (still at the bottom of the page):

```html
<script src="scripts.js"></script> 
```
	
Note that prior to HTML5, an additional `type` attribute was required so you may see external JavaScript files linked this way as well:

```html
<script type="text/javascript" src="scripts.js"></script> 
```

In the external JavaScript file you don't include `<script>` tags, just the JavaScript code itself.
