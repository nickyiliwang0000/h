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
#### `.reduce()`
We give the `.reduce()` method an array and two arguments: the total value (i.e. accumulator) and the current amount (i.e. current value). 

The `.reduce()` method then gives us back (i.e. **returns**) a single value.

Here is an example of an array of numbers that need to be added up:

```js
const nums = [2, 4, 6, 8]
const sum = nums.reduce((total, integer) => {
  return total + integer
});
console.log(sum)
// 20
```

Similar to `.map()`, `.filter()`, and `.forEach()`, the `.reduce()` function expects a callback function as an argument: as the `.reduce()` method cycles through the array (like a `for` loop), the callback function is executed against the _accumulator_ and each element in the array (from left or right) to reduce it to a single value. The accumulator is the parameter on the left in the function passed to `.reduce()`. It's only used inside of the function - kind of like `i` in a `for` loop.

You can also use `.reduce()` on non-numbers:

```js
let words = ['Dear', 'Sir','or','Madam']

let phrase = words.reduce( (phraseSoFar, currentWord) =>{
    return `${phraseSoFar} ${currentWord}`;
  }
)

console.log(phrase);
// "Dear Sir or Madam"
```

Here's another useful example of when we can use `.reduce()` to _flatten_ multiple arrays into one single array.

```javascript
const nums = [[1, 2, 3], [4, 5, 6], [7, 8, 9]];
const flatArray = nums.reduce((total, amount) => {
  return total.concat(amount);
});

// console.log(flatArray)
// [ 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
```

`.reduce()` is often used in combination with other functions to solve complex problems, (e.g. to count [the number of times a string occurs in an array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce#Counting_instances_of_values_in_an_object)).

## TL;DR
Here's a cute little emoji summary [from a developer on Twitter](https://twitter.com/steveluscher/status/741089564329054208) of what each of these methods do.

```bash
map([🌽, 🐮, 🐔], cook)
=> [🍿, 🍔, 🍳]

filter([🍿, 🍔, 🍳], isVegetarian)
=>  [🍿, 🍳]

reduce([🍿, 🍳], eat)
=> 💩
```
<!-- From https://twitter.com/steveluscher/status/741089564329054208 -->

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
