<!-- Student takeaway -->
<!-- By the end of this lesson, the student should know:
- To avoid spaghetti code
- To avoid conflicting code with external libraries
- How to namespace an app
-->
# How to organize your JavaScript

## Avoid spaghetti code
Without any guidelines, it can be difficult to read and trace control flow through long JavaScript files. Many lines of code that are all snarled up and hard to handle are affectionately referred to as "spaghetti code".

If you ever find yourself stuck in a tangle, don't panic. A little _code refactor_ can smooth these issues out. Think of it like ~~copyediting~~ ~~copy-editing~~ copy editing your code.

## Avoid conflicting code

Sometimes without meaning to, developers working on a project months apart or people working on different widgets for the same platform can name their variables or functions the same thing and browser doesn't know which one to use.

Imagine you create a variable to hold your Twitter handle for your contact page but you're also embedding a Twitter widget on your website. You might end up with something like this:

```js
const twitter = 'http://twitter.com'; //created by the widget
/* ... lots of other code ... */
const twitter = '@thisishackeryou'; //created by you
```

Since variables can't be redeclared in JavaScript, we won't have access to our `twitter`! And if we write ` twitter  = '@thisishackeryou';` in our JavaScript file, we might reassign the variable in both files without meaning to.  Again, don't panic, but know that we can fix this through better organization.

## Be mindful of scope
Our sample conflict above is what's called a _scope issue_. 

Variables declared outside of a function are part of the **global** scope. This means they can be accessed (and over-written!) from **anywhere** in your code.

On the other hand, variables declared inside a function have **local** scope. This means they're only available to other code **inside the function**.

For example, the global variable `planet` is accessible within our `whereAmI` function here:

```js
let planet = "Earth";

function whereAmI(){
  console.log(planet);
}

whereAmI(); 
// "Earth"
```

But if we had a locally scoped `planet` variable, it would override the global one:

```js
let planet = "Earth";

function whereAmI(){
  let planet = "Mars";
  console.log(planet);
}

whereAmI(); 
//"Mars"
```

The `destination` variable is locally scoped to the `chooseDestination` function and unavailable in the `launchRocket` function's scope:

```js
function chooseDestination(){
  let destination = "The Moon"
}

function launchRocket(){
  console.log(destination);
}

chooseDestination();
launchRocket(); 
// error
```
More about scope in (this lesson)[https://github.com/HackerYou/bootcamp-notes/blob/master/applied-javascript/advanced-js-lexical-scope-and-execution-context.md].

## Namespacing

To avoid scope issues and help break your code into more modular components, consider writing your code inside a containing object. Start with an empty object that will hold all the application code:

```js
const myApp = {};
```

This creates what's called a _namespace_ for our code. All variables and functions will be properties of that object and so when we declare them we start with the `myApp` namespace, which protects them from conflicts with other code. 

We can now add our Twitter variable as a property on the `myApp` object.

```js
myApp.twitter = 'thisishackeryou';
```

We can store functions in our `myApp` object the same way.

```js
myApp.getTweets = function(){
  //code to retrieve tweets
};
```

We can call this method elsewhere in the app with:

```js
myApp.getTweets();
```

You can add as many variables and functions as you need to keep your code organized into small pieces!

```js
const myApp = {};

myApp.twitterHandle = 'thisishackeryou';
myApp.numberOfTweets = 3;
myApp.includeRetweets = false;

myApp.getTweets = function(){
  //retrieves tweets
}

myApp.displayTweets = function(){
  //prints tweets onto the page
}
```

<!-- ### Terminology reminder
Variables are often referred to as **properties** when stored inside an object.

Functions are often referred to as **methods** when stored inside an object.

 -->
### Namespacing in jQuery

Most apps will have a method called `init` (short for 'intialize') that kicks things off. Anything that needs to happen on page load and most event handlers go in here. It's also a good place to cache jQuery selectors:

```js
const widgetApp = {};

widgetApp.init = function(){
  widgetApp.widgetContainer = $('#widget');
  widgetApp.widgetContainer.addClass('active');
  
  $('a.close').on('click', function(){
    widgetApp.widgetContainer.hide();
  });
}
```

We then call the init function inside a jQuery DOM ready so that it executes on page load:

```js
$(function(){
  widgetApp.init();
});
```

Why only put the `widgetApp.init()` method in the document ready? If we put all our code inside of the `ready` function:

```js
$(function() {
	const widgetApp = {};
	// ... lots of code ...
	widgetApp.init();
});
```

We would never be able to access the `widgetApp` object from out dev tools because it would be scoped to the anonymous handler for the ready event!

Exposing it before the document ready allows us to play around with the object in the console.

## Exercise

To get some experience into how an application could be organized into an object, download [foodAhoy.html](https://hychalknotes.s3.amazonaws.com/foodAhoy.html) and together we'll refactor this code to show how the namespacing pattern can be applied to an application that already exists.
