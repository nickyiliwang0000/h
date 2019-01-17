## jQuery 

#### What is jQuery

jQuery calls itself the "The write less, do more Javascript library."  What does that mean?

Think of jQuery as a collection of helpful pre-written JavaScript code that you can use to quickly solve some common front-end problems.  While you'll probably use a lot jQuery on most of your projects, remember that it's all JavaScript behind the scenes.

#### Why Use jQuery?

There are two main reasons you might want to use jQuery.

##### 1. jQuery shortcuts a lot of common front-end tasks

There are some things you want to do all the time in your front-end JavaScript code, like animating an element open and closed.  jQuery has its own built in functions like `.show()`, `.hide()`, `.slideUp()`, `.fadeOut()` etc. that can do the heavy lifting for you.

##### 2. jQuery irons out a lot of cross browser inconsistencies.

As you've seen with HTML & CSS, each browser interprets your code a little differently.  This is also a problem with JavaScript, so jQuery does a lot of work behind the scenes to make sure the code you write is cross-browser compliant.


#### Terminology Review

jQuery is really one big object with a lot of helpful methods that you get to use. Let's review what those terms mean before we dive in.

**Object**
In JavaScript, an object is a collection of various properties - each property defined by a key value pair.

```js
let pet = {
	species: "cat",
	color: "black",
	name: "Mittens"
}
```

We can recall a property's value with dot notation and the key:

```js
console.log(pet.name); //logs "Mittens"
```

We can also change a property's value with dot notation and assigning a new value.

```js
pet.name = "Spot";
console.log(pet.name); //logs "Spot";
```

**Method**
Functions in JavaScript are cray and can be stored inside properties! When a function lives in side an object, we call it a method.

```js
let pet = {
	species: "cat",
	color: "black",
	name: "Mittens",
	sayHi : function(){
		alert("meow!");
	}
}
```

We call methods with dot notation too. Just make sure to include parentheses.

```js
pet.sayHi(); //alerts "meow!"
```

Sometimes a method will return a value:

```js
let rando = Math.random(); // rando = 0.8 or another random number
```

Sometimes a method takes arguments when called.

```js
let result = Math.sqrt(16); //result = 4
let result = Math.sqrt(15); //result = 3.8729
```

## The DOM

DOM stands for **document object model**, and it represents all the HTML elements on your page. It's represented by a tree structure, where each element is a **node**. You've already seen the DOM when you look at the elements panel in dev tools!

JavaScript can find and modify any DOM node. Some things you might change with JavaScript:

- Update the text inside an element
- Add or remove a class to trigger CSS3 transitions
- Hide or show elements
- Add dynamic HTML to the page

#### Exploring the DOM

We can access the DOM in vanilla JavaScript with the word `document`.

Try typing `document` into the developer tools console.  You get the HTML for the whole page back!

We can access specific parts of the DOM with some built-in JavaScript methods on the `document` object. 

`document.getElementById('myID')` finds an element with the ID of 'myID'

`document.getElementsByTagName('p')` finds the paragraphs

`document.getElementsByClassName('hey')` finds all elements with a class of 'hey'

If you want to be more general, you can use the following: 

`document.querySelector('input[type=submit]')` finds the first matching input[type=submit] 

`document.querySelectorAll('.hey')` also finds all elements with a class of 'hey' (note that this one requires the dot)

The Mozilla Developer Network has [documentation](https://developer.mozilla.org/en-US/docs/Web/API/Document) with information about all of the properties and methods of the `document` object.


**Exercises**:

In these notes, open the console and:

1. get the element with id of "app"
2. get the elements with the class of "wrapper".
3. get all anchor elements on the page.

**Hint**: Don't forget to call your methods on the document object.

The methods above return a DOM object representing the element. If more than one element is found (in the case of class name or tag name for example) then an array of objects is returned.

#### Manipulating the DOM

The Mozilla Developer Network has [great documentation](https://developer.mozilla.org/en-US/docs/Web/API/element) with information about all of the properties and methods of the element objects. We can take our DOM examples from the last exercise further and start changing things.

**Exercises**:

1. Try setting the `outerHTML` property of the first element with a class of `lessonTopic` to the text "Hello World!"
2. Get the `h1` and add a class of `smallcaps` to it.

## jQuery Selectors

Working with the DOM is pretty cool. But we can make it even better with jQuery. The syntax for interacting with the DOM is abstracted away so it is cleaner and we don't have to worry about cross-browser bugs. Let's give it a try.

#### Manipulating the DOM with jQuery

##### Load jQuery
- Open <a href="https://hychalknotes.s3.amazonaws.com/try-jquery.html" class="exercise" download>**try-jquery.html**</a>
- We need to load the jQuery library before we can work with it. A simple way to do this is to use a remote copy via a CDN. Go to jQuery.com and click the download button near the top. If you scroll down you will find a 'Using jQuery with a CDN' header. In that section you will find links for various CDN's, pick one and copy it.

- Aside: CDN stands for "content delivery network". A CDN is a network of computers which provides static resources (images, JavaScript, CSS, etc.) to users based on proximity. The resources are hosted in multiple locations and the closest computer to the user will serve the resource.  CDNs are fast because they allow us to cache our resources, meaning that if both our site and another use `http://cdn.com/jquery.js`, a browser will take notice. If the resource at `http://cdn.com/jquery.js` is still saved on the computer, the browser will just use that version instead of having to download it fresh.

Solution: `<script src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.4/jquery.min.js"></script>`.

##### Test that jQuery is loaded
- Open <a href="https://hychalknotes.s3.amazonaws.com/try-jquery.html" class="exercise" target="_blank">**try-jquery.html**</a> in Chrome. We can test that jQuery has been successfully loaded by going to the console. The console should show no errors. Type `jQuery` into the console and press enter. The return value should be `function (a,b){return new n.fn.init(a,b)}`. This is telling you that **jQuery is a function**. Type `$` and press enter, you should get the same return value. `$` **is an alias for jQuery**, meaning both will do the same thing, $ is just easier and more common to write.

##### Selecting elements
jQuery is a function that is defined with multiple parameters, but they are optional. The `selector` parameter is all we need for the time being. To find an element on the page, we call the jQuery function and pass it a selector that corresponds to the element.

`$(selector);` or `jQuery(selector);`

But what is a selector?

##### jQuery Selectors
jQuery selectors are exactly the same as CSS selectors! So just like CSS we select elements by using classes, IDs, and tag names. All of the existing 20+ types of CSS selectors will totally work in jQuery.

So to find the `h1` element we type `$("h1");` in the console. The return vale is an array with the h1 tag as an element of the array.

![](http://wes.io/U24E/content)

If we use a selector that appears more than once on a page, like span tags:

```
$('span');
```

We will get an array back of multiple items:

![](http://wes.io/U1uo/content)

#### jQuery objects

When we got the above `h1` tag back, it isn't just a plain ol' h1 tag. It's actually something called a **jQuery object** which has a number of **methods** on it. (Remember that methods are just functions that are specific to an object).

jQuery objects are representations of the HTML elements (sometimes referred to as a wrapped set), and they have tons of methods. We'll explore some of these methods together and then we'll show you how to effectively use the jQuery documentation to learn more.

* Let's use jQuery to change the text of the h1 tag. First get the h1 jQuery object with `$("h1")` and then use the `text()` method to set the text. `$("h1").text("New h1 text!");` should do the trick.

* Let's move an element to a different location. The two paragraphs have the class names `firstp` and `secondp` respectively. jQuery objects have a method called `insertAfter()` which takes an element and moves it after another element. `$(".firstp").insertAfter(".secondp");` will do the trick.

* The CSS class `highlight` is already defined. We can add this class to an element with the `addClass()` method. Add the highlight class to the h1 tag. Solution: `$("h1").addClass("highlight");`

* We can remove this class from an element with the `removeClass()` method. Remove the highlight class from the h1 tag. Solution: `$("h1").removeClass("highlight");`. The `toggleClass()` method will toggle the class on and off!

## jQuery Events

### Tutorial: jQuery events

#### Events

With jQuery we can do anything we want in response to an **event**.  In the browser events usually consist of mouse clicks, mouse hovers, scrolling, window resizes, keyboard presses, etc. There are many more events in the browser, but these are the ones we will look at for now. For more events check out this link [here](https://developer.mozilla.org/en-US/docs/Web/Events). The process looks like this:

1. **Event Binding**: attach an event **listener** to a jQuery object with the `on()` method.
2. **Specify the event**: the first argument to the `on()` method is a string (e.g. `"click"`).
3. **Provide Callback Function**: the second argument is an anonymous function with some code that will run once the event happens.

The generic code looks like this:

```js
$(selector).on(event, function(){
	// run this code when event happens
});
```

Or if we wanted to attach an event listener to our `h1` it would look like this.

```js
$('h1').on('click', function() {
	//do something
});
```

Download and open <a href="https://hychalknotes.s3.amazonaws.com/jquery-events.html" class="exercise" download>**jquery-events.html**</a> in your text editor. jQuery has already been loaded for you. We will be writing JavaScript inside of this HTML file so we will run into an issue that we didn't see when working in the console. While in the console all of the code that we wrote was executed after the page was fully loaded. The JavaScript that we will be writing will be loading within the HTML document so there is a chance that it will execute before the page is fully loaded.

If we try to find an element using jQuery before it's loaded, we will get an error. To prevent this from happening we use a jQuery method that will let us know when the document is ready to be manipulated.

Inside the `<script></script>` tags add the following:

```js
$(document).ready(function(){
	// your code here
});
```

So what we are doing is wrapping all of our code inside of an anonymous function. This function will be called once the document is ready.

There are four boxes on the page. We want to hide the boxes when they are clicked. Let's start with the skeleton code for an event.

```js
$(document).ready(function(){
	$(selector).on(event, function(){
		// run this code when event happens
	});
});
```

All of the boxes have the class "box" so we can use that to select them, `$(".box")` should do the trick.

```js
$(document).ready(function(){
	$(".box").on(event, function(){
		// run this code when event happens
	});
});
```

The event we're looking for is a `click`:

```js
$(document).ready(function(){
	$(".box").on("click", function(){
		// run this code when event happens
	});
});
```

jQuery has the method `hide()` that will come in handy. Let's select the box again and hide it.

```js
$(document).ready(function(){
	$(".box").on("click", function(){
		$(".box").hide();
	});
});
```

All of the boxes disappeared! This is because `$(".box")` selects all of the boxes. Ok, how do we select on the box that was clicked? Remember the `this` keyword? jQuery provides `this` inside of the anonymous function as the element we clicked on. How convenient!

```js
$(document).ready(function(){
	$(".box").on("click", function(){
		this.hide();
	});
});
```

Unfortunately `this` isn't a jQuery object, it's a DOM element. We need to convert it into a jQuery object with `$(this)`. If we pass `this` inside of jQuery as a selector we can create a jQuery object from that. 

```js
$(document).ready(function(){
	$(".box").on("click", function(){
		$(this).hide();
	});
});
```