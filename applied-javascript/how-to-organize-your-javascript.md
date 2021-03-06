<!-- Student takeaway -->
<!-- By the end of this lesson, the student should know:
- To avoid spaghetti code
- To avoid conflicting code with external libraries
- How to namespace an app
-->

# How to organize your JavaScript


#### Terminology reminder

Variables are referred to as **properties** when stored inside an object.

Functions are referred to as **methods** when stored inside an object.

OK, let's go!


## JavaScript organization

As you add more lines and functionality to your JS code, it can start to get a little unruly. 


### Problem 1: 'Spaghetti code'

You might have trouble tracking down which lines do what, or you will have a hard time changing or adding new features. If you ever find yourself in an unorganized tangle, you've probably stumbled upon (or written!) what we call spaghetti code. Don't panic! A little code organization can help you steer clear of these issues.


### Problem 2: Conflicting code

Another reason to organize your code is to avoid conflicts with other plugins or libraries that you're running on your website. Say you create a variable to hold your twitter handle for your contact page, but you're also embedding a twitter widget on your website. You might end up with something like this:

```js
let twitter = 'http://twitter.com'; //created by the widget
/* ... lots of other code ... */
twitter = '@junocollege'; //created by you
```

We might have just overwritten and reassigned the widget's variable, and most likely broken it!  Again, we can fix this through better organization.


### Scope

In our sample conflict above, we're running into what's called a scope issue. 

Variables declared outside of a function are part of the **global** scope. This means they can be accessed (and reassigned) from anywhere in your code.

On the other hand, variables declared inside a function have **local** scope. This means they are only accessible within that function's code block.


#### Examples

The global variable `planet` is accessible within the function:

```js
const planet = "Earth";

function whereAmI() {
  console.log(planet);
}

whereAmI(); //logs "Earth"
```

The `planet` variable that is printed is the value that is scoped to the function it was called from:

```js
const planet = "Earth";

function whereAmI(){
  const planet = "Mars";
  console.log(planet);
}

whereAmI(); //logs "Mars"
```

The `destination` variable is locally scoped to the `chooseDestination` function and unavailable in the `launchRocket` function's scope:

```js
function chooseDestination(){
  const destination = "The Moon";
}

function launchRocket(){
  console.log(destination);
}

chooseDestination();
launchRocket(); // gives us an error
```

In the above example the last one is a problem, but this scoped structure can be useful for us if we want to prevent conflicts; we can protect parts of our code by making them unavailable elsewhere in an app.


### Organizing your code with an object

To avoid scope issues and help break your code down into more modular components, we can organize our code using an object. 

We start with an empty object that will hold all our our application code.

```js
const myApp = {};
```

This creates what's called a _namespace_ for our code. All of your global variables and functions will instead be properties and methods on your namespace object, protecting them from conflicts with other code.

WFor example, we can now add our twitter variable as a property on the `myApp` object:

```js
myApp.twitter = '@junocollege';
```

We store our functions in our app object the same way:

```js
myApp.getTweets = function(){
  //code to retrieve tweets
};
```

We can call this function elsewhere in the app with:

```js
myApp.getTweets();
```

You can add as many variables and functions as you need to keep your code organized into small pieces!

```js
const myApp = {};

myApp.twitterHandle = 'junocollege';
myApp.numberOfTweets = 3;
myApp.includeRetweets = false;

myApp.getTweets = function(){
  //retrieves tweets
}

myApp.displayTweets = function(){
  //prints tweets onto the page
}

console.log(myApp);
```

We can write properties outside the namespace object (using the assignment operator) or directly inside it (with object literal notation). Both will achieve the same results, however it is more common to see these properties defined outside the object. As your app gets more complicated, you may find defining the properties outside of the object easier to read.

<table>
<tr>
<th>Creating properties outside the object</th>
<th>Creating properties inside the object</th>
</tr>
<tr>
<td>
<pre lang="js">
const budgetApp = {};
budgetApp.user = null;
budgetApp.budget = 3000;
budgetApp.logIn = function() {
  // sets user to something other than null
}
budgetApp.addExpense = function() {
  // subtract from budget based on user input
}
</pre>
</td>
<td>
<pre lang="js">
const budgetApp = {
  user: null,
  budget: 3000,
  logIn: function () {
    // sets user to something other than null
  },
  addExpense: function() {
    // subtract from budget based on user input
  }
};
</pre>
</td>
</tr>
</table>


### The `init` method

Most apps will have a special `init` method. This will initialize anything that needs to happen on page load, and hold most of our event handlers. This helps ensure that your handlers are called properly, without interference or reliance of other methods. It's also a good place to cache jQuery selectors.

**The name `init` is just a name. You can name the method whatever you'd like,`init` is simply used as a short form for "initialize", since what we are doing is initializing our application.**

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

We then call the init function inside a jQuery DOM ready so that it executes on page load.

```js
$(function(){
  widgetApp.init();
});
```

Why only put the `widgetApp.init()` method in the document ready? Well if we put all our code inside of the ready function, like so:

```js
$(function() {
  const widgetApp = {};
  ...
  widgetApp.init();
});
```

...then we would never be able to access the `widgetApp` object from our devtools, because it would be scoped to the anonymous handler for the ready event.

Exposing it before the document ready allows us to play around with the object in the console.


### Practice

To get some experience into how an application could be organized into an object, download [foodAhoy.html](https://hychalknotes.s3.amazonaws.com/foodAhoy.html).Together we'll refactor this code to show how the namespacing pattern can be applied to an app that already exists.
