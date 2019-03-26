# To-do app code-along

## A to-do app with JavaScript and jQuery

Let's create a to-do app using JavaScript and jQuery, following the steps below.

Open up [to-do-app.html](https://hychalknotes.s3.amazonaws.com/to-do-app.html) in your text editor and a browser. We've loaded in jQuery and gone ahead and added the skeleton markup required for the app.

Here is what we want our app to do:

* Users can enter tasks into the input field and press enter.
* Upon submit we'll take their inputed task and add it as a list-item to the unordered list below the input field.
* When a user clicks on a list-item, a checkbox icon will get filled and the text should turn grey to indicate that the item has been completed.

### Document ready

Let's start by including the document ready script so that we are sure our app will work as expected.

```js
$(document).ready(function(){
  // code goes here
});
``` 

Or use the shorthand version:

```js
$(function(){
  //code goes here
});
```

### Event binding

The first thing we need to do is add an event listener to the form. We want to listen for the `submit` event and then run our code when the form is submitted (i.e. someone pressed enter).

```js
$(function(){
  $('form').on('submit', function() {
    // do something
  });
});
```

For testing purposes let's print something to the console.

```js
$(function(){
  $('form').on('submit', function() {
    console.log("form is submitted!")
  });
});
```

At first this doesn't seem to work and it's hard to debug the issue because we don't see any errors. The problem is that the page is being refreshed when the form submits, this is the default behaviour. So if you look very closely you'll notice that the console shows our printed string for a split second before it is refreshed.

### Prevent default

The default behaviour of a form is to refresh the browser when you submit, so we need to prevent this from happening. The callback function to the event listener can optionally give us access to the event that triggered the function. We just need to pass a parameter into the function like so:

```js
$(function(){
  $('form').on('submit', function(event) {
  // we can now do stuff to the event!
  console.log("form is submitted!")
  });
});
```

Notice that the only difference is the `event` parameter. We can call this anything we want. It's just a variable/parameter that holds the event object. Using either `event` or `e` is acceptable but be sure to stick to one naming convetion for your app. The event has a method called `preventDefault()` which can stop the default behaviour of the `submit` event.

```js
$(function(){
  $('form').on('submit', function(event) {
    event.preventDefault();
    console.log("form is submitted!")
  });
});
```

We should now see `form is submitted!` in the console. This means that we've prevented the form from refreshing the page. 

### Input value

Instead of printing `form is submitted!` lets print the value that the user put in the input field. The [jQuery documentation](https://api.jquery.com/) has an [attributes category](https://api.jquery.com/category/attributes/) which will help here. In there you will find `.val()`. This method will allow us to get the values of form elements.

```js
$(function(){
  $('form').on('submit', function(event) {
    event.preventDefault();

    let toDoItem = $('input').val();
    console.log(toDoItem);
  });
});
```

This works but there is a usability issue. After submitting the form, users would need to empty the input field manually before adding a second item. Let's empty the input field by setting its value to an empty string.

```js
$(function(){
  $('form').on('submit', function(event) {
    event.preventDefault();

    let toDoItem = $('input').val();
    console.log(toDoItem);
    $('input').val('');
  });
});
```

`.val()` is what we call a _getter_ and a _setter_. A getter method can read a value. A setter method can assign a value. So, when the method is called with a value as an argument, it's referred to as a setter since it sets (or assigns) that value. When the method is called with no argument, it gets (or reads) the value.

We should only do something if the input value is not empty, otherwise we would be adding empty items to our list.

```js
$(function(){
  $('form').on('submit', function(event) {
    event.preventDefault();
    let toDoItem = $('input').val();

    if (toDoItem !== '') {
      console.log(toDoItem);
      $('input').val('');
    }
  });
});
```

### Adding HTML elements

Let's construct an HTML string using concatenation that will in the end look like this: `<li> toDoItem </li>`.

```js
$(function(){
  $('form').on('submit', function(event) {
    event.preventDefault();
    let toDoItem = $('input').val();

    if (toDoItem !== '') {			
      console.log("<li>" + toDoItem + "</li>");
      $('input').val('');
    }
  });
});
```

Instead of printing it to the console lets put these list items inside of our unordered list. In the jQuery API look for "Manipulation". The sub-categories are self-explanatory. It should be clear that we're looking for "DOM Insertion, Inside" (because we want to put an element inside of `ul`).

We want to add list items to the end of `ul` so `.append()` will do. If we wanted the latest item to be added to the top then we would use `.prepend()`. Let's find the `ul` element and append the list item inside of it.

```js
$(function(){
  $('form').on('submit', function(event) {
    event.preventDefault();

    if ($('input').val() !== '') {
      let toDoItem = $('input').val();
      $('ul').append("<li>" + toDoItem + "</li>");
      $('input').val('');
    }
  });
});
```

Since we have Font Awesome imported into our app we can add icons indicating that the item is incomplete. `<span class='fa fa-square-o'></span>` will do the trick.

```js
$(function(){
  $('form').on('submit', function(event) {
    event.preventDefault();

    if ($('input').val() !== '') {
      let toDoItem = $('input').val();
      $('ul').append("<li> <span class='fa fa-square-o'></span>" + toDoItem + "</li>");
      $('input').val('');
    }
  });
});
```

### Item completion level 1

A to-do app is no good if we can't check off items. We need a way change the Font Awesome icon class from `fa-square-o` to `fa-check-square-o` when an item is clicked. This means we need another event listener except this time we're listening for a `click` event. Add the following under your existing code (**inside of the document ready but after the `form` listener**):

```js
$('form').on('submit', function(event) {
  ...
});

$('li').on('click', function(){
  // do something here
});
```

Let's print a string to the console again when an item is clicked. *Building code incrementally in small chunks and using the console a lot will ensure that we catch errors and bugs before our code gets too big.*

```js
$('li').on('click', function(){
  console.log("an item was clicked!");
});
```

Nothing is happening. We're clicking on `li` items so why isn't the callback function being triggered? The problem is that the `li` items were added after the DOM was fully loaded. These are dynamic elements, we have no idea when they were added. Event listeners are attached when the DOM fully loads so we can't attach events directly to dynamic elements.

### Event delegation

Remember, [events in JavaScript](https://developer.mozilla.org/en-US/docs/Web/Events#Keyboard_events) are designated actions (e.g. `click`, `mouseover`, `touchstart`, `keypress`, etc). When an action takes place, we usually want to run some code. By default, the browser lets every ancestor of an event's target know that an action took place. This event flow is often referred to as either _event bubbling_ or _event propagation_. Here's an example: 

```html
<ul>
  <li>
    <a href=""> 
      <img src="" alt="" />
    </a>
  </li>
</ul>
```

When a click event is triggered on the `img`, the browser is going to communicate to every parent element (`a`, `li`, `ul`) that this event took place. As a result, the click on the image not only generates a `click` event for the `img` element, but it also generates a `click` event for every parent element. The event is _bubbling_ up through the DOM tree.

We can use this bubbling behaviour to address our issue of not being able to add an event listener to our dynamic `li` elements. We can delegate our click event to a ancestor element that gets loaded with the DOM. `ul` is a good candidate because it is the parent of the `li` elements and it is rendered when the DOM is ready. When someone clicks an `li` element, that click event will bubble up to the `ul`.
We can delegate an event by using the following syntax:

```js
$(**parentElement**).on(**event**, **targetElement**, function(){
  // do something
});
```

Notice that the only difference is that an additional argument is passed to the `on()` method. So binding an event listener on `ul` which triggers when `li` elements are clicked looks like this:

```js
$('ul').on('click', 'li', function(){
  console.log("an item was clicked!");
});
```

To print the item that was clicked we use the `this` keyword.

```js
$('ul').on('click', 'li', function(){
  console.log(this);
});
```

### Item completion level 2

Instead of printing to the console we want to:

1. Find the Font Awesome icon inside of the item. To do that we will need to "traverse" the DOM. The jQuery documentation is helpful by telling us that `.find()` is used to find "descendants of each element in the current set of matched elements".

```js
$('ul').on('click', 'li', function(){
  let checkBox = $(this).find('.fa');
});
```

2. Change the class from `fa-square-o` to `fa-check-square-o`. In the [jQuery documentation](https://api.jquery.com/category/manipulation/class-attribute/) under 'manipulation' we see 'Class Attribute'. This sub-category shows us several useful methods including `.addClass()`, `.removeClass()` and `.toggleClass()`.

```js
$('ul').on('click', 'li', function(){
  let checkBox = $(this).find('.fa');
  checkBox.removeClass('fa-square-o');
  checkBox.addClass('fa-check-square-o');
});
```

### Item completion toggle

What if users change their mind about a completed item? We want them to be able to toggle the check and uncheck Font Awesome icons. `toggleClass()` seems to be a good place to start; what does the documentation say? 

> Add or remove **one or more** classes from each element in the set of matched elements

Hey that sounds promising, we can toggle multiple classes? That's awesome. 👍

```js
$('ul').on('click', 'li', function(){
  let checkBox = $(this).find('.fa');
  checkBox.toggleClass('fa-square-o fa-check-square-o');
});
```

And it works!

### Lots more

We can apply a class named `text-muted` which will help convey meaning to the user through color. Our completed tasks should look inactive when compared to uncompleted tasks.

```js
$('ul').on('click', 'li', function(){
  let checkBox = $(this).find('.fa');
  checkBox.toggleClass('fa-square-o fa-check-square-o');
  $(this).toggleClass('text-muted');
});
```

Have a look at <a download href="https://hychalknotes.s3.amazonaws.com/to-do-app-answer.html" class="exercise">**to-do-app-answer.html**</a> for the complete app. 

### Kicking it up a notch. (BAM!) 💥

There is so much more that you can do to enhance the app! Here are some suggestions:

- allow the removal of items completely from the list
- validate the input field with an error message if the input is empty upon submit
- automatically move completed items to the bottom
- when the page loads, focus on the input field (i.e. cursor should load inside the input)
- check out [jQuery UI](https://jqueryui.com/) to drag/drop items to sort

Have a look at [to-do-app-extras.html](https://hychalknotes.s3.amazonaws.com/to-do-app-extras.html) to see the solution to the above extras. Can you think of something not on the list? Try to personalize your app.
