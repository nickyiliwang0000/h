<!-- Student takeaway -->
<!-- By the end of this lesson, the student should know:
- That data is inherently mutable
- What 3 things .map(), .filter(), and .reduce() have in common? (return something, don't mutate data, take a callback function)
- That Underscore and other JS libraries exist
-->

# Advanced array methods

The methods and libraries we will be looking at in this section are part of a programming paradigm called _functional programming_. It's the idea that a developer should have the proper tools (i.e. functions) on hand to accomplish a task.

## Working with data

When working with data, we often need to tweak, bend, and reorganize it to suit our needs. Not every array is exactly what we need for every purpose. Sometimes we don't control the organization of the data, as in the case of returned data from external APIs. We need to be able to adapt and manipulate data into the structures that our project requires.

There are useful native JavaScript methods and powerful external libraries that exist to help us accomplish these tasks. Some of these methods could be replaced by some creative iteration and reworking of arrays using methods - remember that there are always many ways to do something in JavaScript!

<!-- We'll be going over a few super useful methods and you can [follow along using this file](https://hychalknotes.s3.amazonaws.com/advanced-array-methods-exercises.html). -->

We'll be going over a few super useful methods, so open up a new HTML document and follow along. 
<!-- and you can [follow along using this file](https://hychalknotes.s3.amazonaws.com/advanced-array-methods-exercises.html). -->

### Our friend `.forEach()`
The `.forEach()` method iterates over an array and performs a provided task (i.e. a callback function). Within the callback, we can define two arguments that represent the iterated item's _value_ and _index_.

`.forEach()` does not return a new array.

Let's say we wanted to display a list of movie genres to our movie catalogue website. We have a `div` that looks like this:

```html
<div class="movieGenres">
</div>
```

We can use `.forEach()` to append each movie genre to the `movieGenres` container one at a time:

```javascript
const genres = ["Horror", "Comedy", "Drama", "Action", "Suspense", "Documentary"];

genres.forEach((genre) =>  {
  $(".movieGenres").append("<p>" + genre + "</p>");
});
```

This is the same thing as:
```js
const addMovieGenre = function(array){
  for (let i=0; i<array.length; i++){
    $(".movieGenres").append("<p>" + array[i] + "</p>");
  }
}
```

### More native methods
The following methods are included (among others) in JavaScript to help sort data: `.filter()` `.map()` and `.reduce()`.

<!-- `.map()`, `.filter()` and `.reduce()` are considered pure functions.  -->
Each of these methods iterates over an array or object in a slightly different way. But two things all these methods have in common are:
1. each one uses a callback function to define the task to be performed on the data 
1. each one returns something (an array or a value) instead of changing the array provided to it

#### `.map()`
We give the `.map()` method an array and a set of directions (i.e. a **callback function**) about what to do with each item in that array. The `.map()` method then gives us back (i.e. **returns**) an array of each item with the thing done to it. Because it returns an array, it's smart to store the return in a variable.

**Dividing values in an array:**
```js
const numbers = [10, 100, 25, 20];

const halfNumbers = numbers.map(function(value) {
  return value / 2;
});

console.log(halfNumbers);
//[5, 50, 12.5, 10];
console.log(numbers);
//[10, 100, 25, 20]
```

The `.map()` method will run a function for every element in the array, and it will allow you to mutate the new data however you like. Notice that `numbers`, the original array, is not changed.

**Creating an array of items from objects:**
```js
const persons = [
  {first: 'Sanjay', last: 'Patel'},
  {first: 'Ash', last: 'Ketchum'},
  {first: 'Hermione', last: 'Granger'}
];

const people = persons.map((value) =>  {
  return value.first + ' ' + value.last;
});

console.log(people);
//["Sanjay Patel", "Ash Ketchum", "Hermione Granger"]

```

#### `.filter()`

We give the `.filter()` method an array and a filtering condition (i.e. a **callback function**). The `.filter()` method then gives us back (i.e. **returns**) an array of each item that fulfilled (i.e. returned `true`) the condition. Again, because it returns an array, it's smart to store the return in a variable.

**Filtering out users who are younger than 18:**
```js

const users = [
  { name: 'Spider-Man', age: 16 },
  { name: 'Buffy Summers', age: 25 },
  { name: 'Gandalf the Grey', age: 90 },
  { name: 'Arthur Read', age: 9 }
];

const votingAge = users.filter((value) => {
  return value.age >= 18
});

console.log(votingAge);
//[
//  { name: 'Buffy Summers', age: 25 },
//  { name: 'Gandalf the Grey', age: 90 }
//];

```

**Filter song titles longer than 8 characters:**

```js
const songs = ["Pain", "Sweetness", "Work", "The Middle", "I Will Steal You Back"];

const longTitles = songs.filter((value) => {
  return value.length >= 8;
});

// longTitles = ["Sweetness", "The Middle", "I Will Steal You Back"]
```

## Resources and concepts: 
<!-- * Video: [Functional Programming in JavaScript](https://www.youtube.com/playlist?list=PL0zVEGEvSaeEd9hlmCXrk5yUyqUag-n84) -->
* Article: [Functions as first class citizens](http://ryanchristiani.com/functions-as-first-class-citizens-in-javascript/)
* Check out these [great videos](https://www.youtube.com/playlist?list=PL0zVEGEvSaeEd9hlmCXrk5yUyqUag-n84) on YouTube for more information about functional programming!
* For more information on the iteration methods available within native JavaScript, read [this article](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array#Iteration_methods) on MDN. 
  * Be aware that all methods below don't work in all browsers. The ones we used today won't work in IE9+ and some newer methods may not work in anything bleeding edge versions of modern browsers.
* To get more familiar with the functional methods try [these exercises](https://github.com/Rchristiani/functional-exercises).

### Beyond native methods and Underscore.js, some other libraries include the following:

* [is.js](https://arasatasaygin.github.io/is.js/) - a microcheck library for checking values
* [Ramda](http://ramdajs.com/0.18.0/index.html) - A library of functional programming methods
* [LoDash](https://lodash.com/) - Similar data transformation library to Underscore.js

## Function methods code-along

To further practice, let's use jQuery and these new methods to populate this app. [Download the exercise here](https://hychalknotes.s3.amazonaws.com/functional-methods-codealong.zip).
