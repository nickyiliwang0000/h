<!-- Student takeaway -->
<!-- By the end of this lesson, the student should know:
- That data is inherently mutable
- What 3 things .map(), .filter(), and .reduce() have in common? (return a new array, don't mutate data, take a callback function)
- That Underscore, and other JS libraries exist
- 
-->

# Advanced array methods

The methods and libraries we will be looking at in this section are part of a programming paradigm called _functional programming_. Although it sounds fancy and maybe a little scary, think of functional programming as a way to use functions to transform data.

## Working with data

When working with data, we often need to tweak, bend, and reorganize it to suit our needs. Not every array is exactly what we need for every purpose. Sometimes we don't control the organization of the data, as in the case of returned data from external APIs. We need to be able to adapt and manipulate data into the structures that our project requires.

There are useful native JavaScript methods and powerful external libraries that exist to help us accomplish these tasks. Some of these methods could be replaced by some creative iteration and reworking of arrays using methods - remember that there are always many ways to do something in JavaScript!

We'll be going over a few super useful methods and you can [follow along using this file](https://hychalknotes.s3.amazonaws.com/advanced-array-methods-exercises.html).

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

### More native methods
The following methods are included in JavaScript (among others) to help sort data: `.filter()` `.map()` and `.reduce()`.

<!-- `.map()`, `.filter()` and `.reduce()` are considered pure functions.  -->
Each of these methods iterates over an array or object in a slightly different way. But two things all these methods have in common are:
1. each one uses a callback function to define the task to be performed on the data 
1. each method returns a new array instead of changing the array provided to it

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
  {first: 'Taylor', last: 'Swift'},
  {first: 'Ash', last: 'Ketchum'},
  {first: 'Hermione', last: 'Granger'}
];

const people = persons.map((value) =>  {
  return value.first + ' ' + value.last;
});

console.log(people);
//["Taylor Swift", "Ash Ketchum", "Hermione Granger"]

```

#### `.filter()`

We give the `.filter()` method an array and a filtering condition (i.e. a **callback function**). The `.filter()` method then gives us back (i.e. **returns**) an array of each item that fulfilled (i.e. returned `true`) the condition. Again, because it returns an array, it's smart to store the return in a variable.

**Filtering out users who are younger than 19:**
```js

const users = [
  { name: 'Spider-Man', age: 16 },
  { name: 'Buffy Summers', age: 25 },
  { name: 'Gandalf the Grey', age: 90 },
  { name: 'Arthur Read', age: 9 }
];

const ofAge = users.filter((value) => {
  return value.age >= 19
});

console.log(ofAge);
//[
//  { name: 'Buffy Summers', age: 25 },
//  { name: 'Gandalf the Grey', age: 90 }
//];

```

**Filter titles longer than 8 characters:**

```js
const posts = ["Pain", "Sweetness", "Work", "The Middle", "I Will Steal You Back"];

const longTitles = posts.filter((value) => {
  return value.length >= 8;
});

// longTitles = ["Sweetness", "The Middle", "I Will Steal You Back"]

```
#### `.reduce()`
We give the `.reduce()` method an array and two arguments: the total value (i.e. accumulator) and the current amount (i.e. current value). 

The `.reduce()` method then gives us back (i.e. **returns**) a single value.

Here is an example of an array of numbers that need to be added up:

```javascript
const nums = [2, 4, 6, 8]
const sum = nums.reduce((total, integer) => {
  return total + integer
});
```
```js
console.log(sum)
// 20
```
Similar to a `.map()`, `.filter()`, and `.forEach()`, this method contains a callback function: as the `.reduce()` method cycles through the array (like a `for` loop),  the callback function is executed against the _accumulator_ and each element in the array (from left or right) to reduce it to a single value.

Here's another useful example of when we can use `.reduce()` to _flatten_ multiple arrays into one single array.

```javascript
const nums = [[1, 2, 3], [4, 5, 6], [7, 8, 9]];
const flatArray = nums.reduce((total, amount) => {
  return total.concat(amount);
});

// console.log(flatArray)
// [ 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
```

You can use `.reduce()` with non-numbers: to count [the number of times a string occurs in an array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce#Counting_instances_of_values_in_an_object); `.reduce()` is often used in combination with other functions to solve complex problems, so we've just done the simpler number examples here.

## Underscore.js

Sometimes, your native methods aren't enough. In those times, you might turn to a library like [Underscore.js](http://underscorejs.org). Much like jQuery, Underscore provides helpful shortcuts and tools, specifically for working with data.

Underscore is organized into methods for working with [collections of data](http://underscorejs.org/#collections), [arrays](http://underscorejs.org/#arrays), [objects](http://underscorejs.org/#objects) and [functions](http://underscorejs.org/#functions). To use the library, include a link to the library in your HTML, ideally from a [CDN](http://cdnjs.com/libraries/underscore.js/) and before your scripts.

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/underscore.js/1.8.3/underscore-min.js"></script>
```

All the methods are part of an object named `_`. Similar to how everything from jQuery is on the `$` object. Whenever we call an Underscore method, we start with the `_` and pass in arguments. With all methods, it's possible to pass in a callback function that handles the resulting task.

### _.find()

The `_.find()` method iterates over a list and returns the first value that passes a test. If no result is found, it returns `undefined`, otherwise it continues until the first result is found.

**Find the first value that starts with "A":**

```js
const users = ["Shanley", "Aladdin", "Carrie", "Jian", "Zelalem", "Adonai", "Kimmy"];

const firstName = _.find(users, function(value) {
  return value.charAt(0) === "A"
});

console.log(firstName)
//"Aladdin"

```

### _.where()

The `_.where()` method iterates over each value in a list, and returns an array of all the values that match the provided argument to search for. The argument provided is an object that will be used according to the search guidelines.

**Sort data by year:**

```js
const data = [ 
    { firstName: 'Oldest Kid', year: 1984 },
    { firstName: 'Middle Kid (Twin 1)', year: 1985 },
    { firstName: 'Middle Kid (Twin 2)', year: 1985 },
    { firstName: 'Baby', year: 1987}
];

const eightyFour = _.where(data, {year: 1984});
const eightyFive = _.where(data, {year: 1985});
```

### _.pluck()

Much like the native `.map()` method, `_.pluck()` allows the creation of a new array by searching for a single property name and returning a new array. This is useful when you want to have an array with only specific information while retaining the original collection.

Although, if you need to provide multiple properties, **the map method is your best bet.**

**Creating a new array with only the names of from each object:**
```js

const data = [ 
    { firstName: 'Oldest Kid', year: 1984 },
    { firstName: 'Baby', year: 1987},
    { firstName: 'Middle Kid (Twin 1)', year: 1985 },
    { firstName: 'Middle Kid (Twin 1)', year: 1985 },
    { firstName: 'Baby', year: 1987}
];

const names = _.pluck(data, 'firstName');
console.log(names)
// ['Oldest Kid', 'Middle Kid (Twin 1)', 'Middle Kid (Twin 1)', 'Baby']
```

### _.uniq()

The `_.uniq()` method is useful in that it helps to remove duplicates within an array. By simply passing an array, it will sort and remove all duplicates, or a function can be passed that defines what duplicates to search for.

### Examples

**Removing duplicate names:**

```js
const users = ["Delaney", "Xiao", "Anais", "Delaney", "Parvati", "Jo", "Anais"];

const clean = _.uniq(users);

console.log(clean);
//["Delaney", "Xiao", "Anais", "Parvati", "Jo"]
```

**Removing objects that appear twice:**

```js
const data = [ 
    { firstName: 'Jowoo', year: 1984 },
    { firstName: 'Shawn', year: 1985 },
    { firstName: 'Heloise', year: 1985 },
    { firstName: 'Jowoo', year: 1984 },
    { firstName: 'Heloise', year: 1985 },
    { firstName: 'KP', year: 1987}
];

const cleaned = _.uniq(data, function(value) {
    return value.firstName;
});
// 'Jowoo', 'Shawn', 'Heloise', 'KP'
```

### _.first(), _.last(), _.initial() and _.rest()

These four methods return either the first or last values in an array, or a number of items from the beginning or the end.

For the next few examples, the following example array will be used.

```js
const data = [100, "Dog", true, 14, undefined];
```

#### _.first()
Returns the first element of an array, or passing an argument will return the first X number of items from the array.

```js
const firstTwo = _.first(data, 2);

// firstTwo = [100, "Dog"]
```

#### _.last()
Returns the last element of an array, or passing an argument will return the last X number of items from the end of the array

```js
const lastThree = _.last(data, 3);

// lastThree = [true, 14, undefined];
```


#### _.initial()
Returns everything but the last entry of the array.  Passing an argument will exclude the last X elements from the result.

```js
const firstNums = _.initial(data);
// firstNums = [100, "Dog", true, 14]

let allButTheLastTwo = _.initial(data, 2);
// allButTheLastTwo = [100, "Dog", true]
```

#### _.rest()
Returns everything but the first entry of an array. Passing an argument will return items from that index number forward

```js
const allButFirst = _.rest(data);
// allButFirst = ["Dog", true, 14, undefined]

const fourthOnward = _.rest(data, 3);
// fourthOnward = [14, undefined]
```

## Moving forward 

All of the above tools fall under the umbrella of functional programming: the idea that a developer should have the proper tools (functions) on hand to accomplish a task.

## Resources and concepts: 
* Video: [Functional Programming in Javascript](https://www.youtube.com/playlist?list=PL0zVEGEvSaeEd9hlmCXrk5yUyqUag-n84)
* Article: [Functions as first class citizens](http://ryanchristiani.com/functions-as-first-class-citizens-in-javascript/)
* Article: [Call and Apply for beginners](http://ryanchristiani.com/call-and-apply-for-beginners/)

* Check out these [great videos](https://www.youtube.com/playlist?list=PL0zVEGEvSaeEd9hlmCXrk5yUyqUag-n84) on YouTube for more information about functional programming!

* For more information on the iteration methods available within native JavaScript, read [this article](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array#Iteration_methods) on MDN. 
  * Be aware that all methods below don't work in all browsers. The ones we used today won't work in IE9+ and some newer methods may not work in anything bleeding edge versions of modern browsers.

### Beyond native methods and Underscore.js, some other libraries include the following:

* [is.js](https://arasatasaygin.github.io/is.js/) - a microcheck library for checking values
* [Ramda](http://ramdajs.com/0.18.0/index.html) - A library of functional programming methods
* [LoDash](https://lodash.com/) - Similar data transformation library to Underscore.js

To get more familiar with the functional methods try [these exercises](https://github.com/Rchristiani/functional-exercises).

## Filtering exercise

To further practice, let's use jQuery and some functional methods to populate this app. [Download the exercise here](https://hychalknotes.s3.amazonaws.com/functional-methods-codealong.zip).