# jQuery best practices

As you start to write more and more jQuery code, it's a good idea to use some best practices to help your code be more efficient and organized. Developers ❤️ efficiency! Here are a few of our favourite techniques.

## Cache your selectors

Whenever we use jQuery's `$` selector, jQuery searches through your page for all possible matches.  If you have a large site, a simple selector like `$('.box')` might take a long time and slow down your site, especially if you do it more than once. If you need to work with DOM elements more than once, you can hold onto them the first time they're found by storing them in a variable. In jQuery lingo, we call this _caching your selectors_

**Incorrect 👎**

```js
$('.box').addClass('square');
$('.box').css('color', 'green');
$('.box').html('<p>This is a box.</p>');
```

**Correct 👍**

```js
//find all elements with a class of box and cache them
let $boxes = $('.box');
$boxes.addClass('square');
$boxes.css('color', 'green');
$boxes.html('<p>This is a box.</p>');
```

Note that it's common practice to name your variables starting with a '$' if they are holding jQuery objects.  It serves as a helpful reminder that you can use all the amazing jQuery methods on this variable.

```js
let $listItems = $('li');
let favouriteColour = "salmon";
```

## Chain your methods

A lot of jQuery methods will return the original object that you were working with. 

`$('#widget').addClass('active'); //returns $('#widget')`

Huh? Think of the above example this way: You hand off your `div#widget` to jQuery and ask jQuery to add a class to it; jQuery does so, then it hands the `div` back to you (with the newly added class).
This is significant, because now that you have the widget again, you could potentially hand it back to jQuery and ask it to do something else as well, like change the text inside it. This can go on as many times as you like, as long as you're using methods that return the original object back to you.

When we keep asking jQuery to do more things in the same transaction, it's called _chaining_.

```js
$('#widget').addClass('active').text('It was a dark and stormy night').css('background', 'grey');
//is shorthand for
$('#widget').addClass('active');
$('#widget').text('It was a dark and stormy night');
$('#widget').css('background', 'grey');
```

This can improve readability of your code and is also another technique to cache a selector.

Note that you could also write the above chained method calls like this:

```js
$('#widget')
	.addClass('active')
	.text('It was a dark and stormy night')
	.css('background', 'grey');
```

Until you add the `;` at the end of the line, and as long as there is a `.` at the start of the next line, it will keep working!