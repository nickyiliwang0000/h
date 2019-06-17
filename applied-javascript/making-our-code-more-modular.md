  <!-- Student takeaway -->
  <!-- By the end of this lesson, the student should know:
  - What a module is
  - How to create a default
  - How to create a named export
  - How to import a named or default export
  - That you can rename an import
  - That npm is a way to get access to public modules
  -->

# Making our code more modular
As we write more and more JavaScript, our code runs the risk of becoming unwieldy.

When we ran into this problem in CSS, we turned to Sass and we were able to solve this issue by creating partials. In JavaScript, we solve this by using _modules_!

## What are modules?

Modules are smallish chunks of code stored in separate files that can be composed together. (Kind of like Lego blocks.) Modules are easier to manage and understand than single files that are hundreds or even thousands of lines long.

Think back to when we were creating our API projects. We had one giant object that had lots of methods and properties stored on it. By the end of your project, it was probably over a hundred lines long. Imagine we were accessing multiple different APIs, or had a few separate applications that we were all trying to store in one file. Yiiiikes.

The separate, small modules are grouped together in a process called _bundling_ so that we can use them on our websites.

## How do we use modules?

Modules aren't natively supported by all browsers. But they are supported by Firefox 63+, so let's take a look at how they work:

Download [learning-modules.zip](https://hychalknotes.s3.amazonaws.com/learning-modules.zip) to follow along.

### Set up 
To start, we need to include a `type` attribute whose value is `module` on our script tag.

```javascript
<script type="module" src="scripts/app.js"></script>
``` 
<!-- Should there be more here? -->

### Building and exporting a module
Let's imagine that we're building a program that requires a couple different kinds of randomization (e.g. random day of the week, random number, random color code, etc.).

We're going to create a module to store our randomizing functions. Let's create a file called `randomizer.js` in our scripts folder. This will be our module.

```bash
- learning-modules
  index.html
  - scripts 
    app.js
    randomizer.js
```

Let's start by writing the randomizing function in `randomizer.js` as if it were any other JavaScript file:

```javascript
// randomizer.js

const days = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday'];

function getRandomDay() {
  const randomDay = Math.floor(Math.random() * days.length);

  return days[randomDay];
}
```

Awesome! Now we have to find a way to tell JavaScript that we want to be able to use this code in another file.

For that, we have the `export` and `default` keywords.

```javascript
// randomizer.js

const days = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday'];

export default function getRandomDay() {
  const randomDay = Math.floor(Math.random() * days.length);

  return days[randomDay];
}
```

`export default` tells any files that want to import our `randomizer.js` module that we want them to have access to our `getRandomDay` function.

> Note that you can only have **one** default export per module.

Hooray, we made a module! Now we can use it in our main application.

### Importing your modules using `import`

Let's hop over into `app.js` and imagine that we're beginning to write our application. We want to bring in our randomizer module so we can take advantage of the `getRandomDay` function we wrote.

Our function is ready to use because of the `export` keyword. To use it, we need to the `import` keyword!

```javascript
// app.js
import getRandomDay from './randomizer.js';

getRandomDay(); // Wednesday

```

Ta-da! We have successfully imported our `getRandomDay` function.

`import` allows us to dig into our `randomizer.js` module and pull out whatever was set as our default export (which, you'll remember, was `getRandomDay`!).

Imagine you wrote your `app.js` code a long time ago and already created a function in it called `getRandomDay`. Uh-oh! Do we have to change the name of the function in the module? 

Nope! We can rename the imported `getRandomDay` function in our `app.js` to anything we want. This...

```javascript
// app.js
import randomFunctionName from './randomizer.js';
```
...is the same as this:
```javascript
import getRandomDay from './randomizer.js';
```
The only difference for you is that when you call the function in `app.js`, you must call it by the name you chose when it was imported.

### Importing and exporting named functions

#### Exporting named functions
Let's say we want to add another randomization function to our module; one that prints out a random number between one and 100:

```javascript
//randomizer.js
const days = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday'];

export default function getRandomDay() {
  const randomDay = Math.floor(Math.random() * days.length);

  return days[randomDay];
}

function getRandomNumber() {
  return Math.round(Math.random() * 100);
}
```

Since modules are only allowed to have one default export, how are we going to export our `getRandomNumber` function? Like this:

```javascript
//randomizer.js
const days = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday'];

export default function getRandomDay() {
  const randomDay = Math.floor(Math.random() * days.length);

  return days[randomDay];
}

export function getRandomNumber() {
  return Math.round(Math.random() * 100);
}
```
Modules support named exports for functions other than the default. When we use the `export` function **without** the `default` keyword, we are creating a `named export`.

#### Importing named functions

Importing our named export is similar to importing a default export. It looks like this:

```javascript
// app.js
import { getRandomNumber } from './randomizer.js';

console.log(getRandomNumber()); // 47

```

We place the name of the function that we want to import from the `randomizer` module inside the curly brackets. You'll remember this syntax [from a previous lesson](https://github.com/HackerYou/bootcamp-notes/blob/master/applied-javascript/advanced-js-destructuring-mutability-and-purity.md#destructuring-objects). It was new in ES6 and is called **destructuring**. We're plucking **only** the `getRandomNumber` function out of the `randomizer.js` file.

Now you know how to recognize and implement ES6 modules. 💪 Way to go!

## How we'll use modules in the future
Moving forward, we're going to become very familiar with the _Node package manager_, which is a tool that allows us to access a database of modules written by many developers all over the world. The primary way we'll interact with the Node package manager is through a command line client called `npm`. We're familiar with `git` commands; `npm` commands are quite similar. To retreive a module and download it for your project, you'll be using the `npm install` command. 

[_Node.js_](https://nodejs.org/en/) is a JavaScript runtime environment. It's not imperative that you completely understand Node to be able to use it: for our purposes, think of Node as a way of running programs written **entirely** in JavaScript on your computer (as opposed to the websites we're familiar with, which require an HTML file to link to a JavaScript file).

## Resources
* [Let's Learn ES6: Modules](https://www.youtube.com/watch?v=aQr2bV1BPyE) with Ryan Christiani
* [An Intro to Using npm and ES6 Modules for Front End Development](http://wesbos.com/javascript-modules/) An introd to ES6 modules by Wes Bos
* [An comprehensive discussion of npm basics](https://www.sitepoint.com/beginners-guide-node-package-manager/) (it says for beginners but it's closer to intermediate).
* [The Wikipedia for Node.js](https://en.wikipedia.org/wiki/Node.js) does a better job of explaining what it is than Node's website does.
