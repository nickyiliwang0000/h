<!-- Student takeaway: -->
<!-- At the end of this lesson, the student will be able to:
- Pluck a value from an object with destructuring
- Pluck a value from an array with destructuring
- Explain what mutability is
- Identify a pure function
- Identify an impure function
 -->
# Advanced JavaScript: destructuring, mutability, and purity
As we move forward in JavaScript, we're going to need some new tools and concepts. 

## Destructuring objects
There's a new (in ES6), quick way to grab properties from objects or arrays called _destructuring_.

Say we have an object that looks like this:

```javascript
const pizza = {
  size: 'xl',
  slices: 8,
  type: 'vegetarian'
}
```

Now imagine we want to grab all the properties inside that object and store them in variables. In the past, we would have done this:

```javascript
const size = pizza.size;
const slices = pizza.slices;
const type = pizza.type;
console.log(`One ${size} ${type} pizza with ${slices} slices coming up!`);
// One xl vegetarian pizza with 8 slices coming up!
```

With ES6, we can destructure our pizza object like this:

```javascript
const { size, slices, type } = pizza;

console.log(`One ${size} ${type} pizza with ${slices} slices coming up!`);
// One xl vegetarian pizza with 8 slices coming up!

```

The curly brackets on the left might make you think that this is some kind of object, but don't be fooled! It's just our way of telling JavaScript to pluck the `size`, `slices`, and `type` variable out of the `pizza` object and store them locally.

Remember, 'cause this might trip you up: when destructuring, the word on the **right hand** side of the assignment (in this case, `pizza`), is the thing you want to destructure, and the words between the curly brackets on the **left hand** side (`size`, `slices`, `type`) are the properties you want to pull out of the object.

## Cool. How do I use this?

Writing fewer lines of code is nice, but when might you use this yourself? Well, if you remember back to your API projects, chances are you were getting a big object back from the REST API that looked maybe something like this:

```javascript
// Let's say the JSON Object that we get back from our API looks like this:

{ 'cities' : {
    'toronto':{
      country:'canada',
      population:1200,
      weather:'temperate',
      food:'poutine' 
    },
    'berlin':{
      country:'germany',
      population:1900,
      weather:'temperate',
      food:'donair'
    },
    'sydney':{
      country:'australia',
      population:1000,
      weather:'warm',
      food:'ramen'
    }
  }
}

// And we pass that object to our displayResults function

const displayResults = function(response) {
  const country = response.cities.berlin.country;
  const population = response.cities.berlin.population;
  const weather = response.cities.berlin.weather;
  const food = response.cities.berlin.food;

  console.log(`Berlin is a city of ${population} people in ${country}, where they like to eat ${food} in a ${weather} climate.`);  
}
```

Kind of long and annoying. Instead, with destructuring, we can do this!
```javascript
// again, our JSON object from the API

{ 'cities' : {
    'toronto':{
      country:'canada',
      population:1200,
      weather:'temperate',
      food:'poutine' 
    },
    'berlin':{
      country:'germany',
      population:1900,
      weather:'temperate',
      food:'donair'
    },
    'sydney':{
      country:'australia',
      population:1000,
      weather:'warm',
      food:'ramen'
    }
  }
}

// And our new displayResults function using destructuring
const displayResults = function(response) {
  response = response.cities.berlin
  const { food, country, weather, population } = response;
  console.log(`Berlin is a city of ${population} people in ${country}, where they like to eat ${food} in a ${weather} climate.`); 
}
```

Pretty cool, right? If we refactored our API call to **only** return the information for Berlin, we can go **even more** abstract and do the destructuring inside the function parameters!

```javascript
// Here we made a **brand new** API call that gives us back only the entry for 'berlin'
{
  country:'germany',
  population:1900,
  weather:'temperate',
  food:'donair'
}

const displayResults = function({ food, population, weather, country }) {
  console.log(`Berlin is a city of ${population} people in ${country}, where they like to eat ${food} in a ${weather} climate.`); }
```

Woah!!

## Destructuring arrays

Destructuring can also be used on an array. Let's say we have an array of pizza toppings, like this:

```javascript
const toppings = ["pepperoni", "green pepper", "mushroom"];
```
We can destructure this array in the same way we destructured the previous object:

```javascript
const toppings = ["pepperoni", "green pepper", "mushroom"];

const [toppingOne, toppingTwo] = toppings;

console.log(toppingOne, toppingTwo); // pepperoni, green pepper
```

You don't have to grab every item out of the array this one, only as many as you want to use.

If you want to only grab say the third item in the array, you can add commas in to skip items in the array, like so:

```javascript
const toppings = ["pepperoni", "green pepper", "mushroom"];

const [,,toppingThree] = toppings;

console.log(toppingThree); // mushroom
```
Check out [this article](https://codeburst.io/es6-destructuring-the-complete-guide-7f842d08b98f) for more info on destructuring!

## Immutability and purity
These are two programming concepts we've been working with without knowing it! They'll become even more important in React. 

### Immutability

An _immutable_ data structure doesn't change: you get the data once and that's what it is.

A _mutable_ data structure can be changed: you can add to it, remove from it, or change the values in it.

Data and variables are inherently mutable. Mutating data directly can be dangerous because we can lose track of what the original data set looked like. 

Here are examples using `.splice()` and `.slice()` to illustrate the mutability of data:

**Mutable:** 
```javascript
const zoo = ['giraffe', 'monkey', 'lion', 'panda', 'hippo']
zoo.splice(2, 1)  // remove 1 item at 2-index position (that is 'lion')

//zoo contains ['giraffe', 'monkey', 'panda', 'hippo']
```
In the above example, we no longer have access to our original `zoo` array, only to the modified version. We would say that the `zoo` array is mutable.

**Immutable:**
```javascript
const zoo = ['giraffe', 'monkey', 'lion', 'panda', 'hippo'];
const newZoo = zoo.slice(1, 3)

//zoo contains ['giraffe', 'monkey', 'lion', 'panda', 'hippo']
//newZoo contains ['monkey', 'lion']
```
Here, we have access to both the original `zoo` array AND our new version. The original `zoo` array is mutable (i.e. can be changed), but the method `.slice()` has not changed it. The `.slice()` method returns a copy of the original array that has been changed in some way. So, we say that we have kept the `zoo` array immutable (i.e. it has not/will not be changed).

The idea of immutability is part of the functional programming paradigm.

### Purity
You may have noticed that whether the data is mutable or immutable depends on the method applied to it. Functions that change data outside their lexical scope (i.e. functions that **mutate** external data) are known as _impure_ functions. 
> Reread the [scope and execution context lesson](https://github.com/HackerYou/bootcamp-notes/blob/master/applied-javascript/advanced-js-lexical-scope-and-execution-context.md) for more on scope. 

A _pure_ function will always return the same value if provided with the same input value(s). Pure functions don't have any unwanted side effects, such as changing anything in the global scope (outside of the function). 

**Pure function:**
```javascript
function add(a,b) {
  return a + b;
}
const total = add(2,3);
```
Here, `add(2,3)` will always return `5`.

**Impure function:**
```javascript

let total = 0;

function add(a,b) {
  total = a + b;
}
add(2,3);
console.log(total);
```

Here, `add(2,3)` could return any number, because `total` can be reset outside the `add()` function.

> You already know some pure functions! `.map()`, `.filter()` and `.reduce()`!

These concepts are provided as the building blocks to more understanding in the future, so definitely do research (write a blog post!), talk to instructors, and talk to each other about them.