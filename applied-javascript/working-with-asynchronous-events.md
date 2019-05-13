<!-- Student takeaway -->
<!-- By the end of this lesson, the student should know:
- That a promise is not a value: it is the promise of a future value
- How to store the return of $.ajax in a variable
- Why to store the return of $.ajax in a variable
- That promises have success and failure functions
- Rest parameters create an array of arguments that have been passed into a function
- The spread operator passes each item in an array to a function individually in succession
- Async await is a bonus
-->
# Working with asynchronous events
## The problem
Let's say we're building an app that makes two AJAX requests: one for the weather and one for recipes based on the weather. 

We **could** run the first AJAX request and put the second AJAX request in its callback, so that the second AJAX request only runs when the first one is done. That would look like this:

```js
$.ajax({
  url: 'https://www.weather.com/toronto',
  type: 'GET',
  dataType: 'jsonp'
}).then((weatherConditions) => {
  $.ajax({
    url: 'https://api.recipes.com/'+ weatherConditions,
    type: 'GET',
    dataType: 'jsonp'
  }).then((data) => {
    // do something
  });
});
```
This isn't ideal because we need to wait for the response from `https://www.weather.com/toronto` to come back before we can make a call to `https://api.recipes.com/`, which could be a long time. Also, what if we had to complete 10 API calls in sequence?  

Something like this:
```js
$.ajax({
  url: 'https://www.weather.com/toronto',
  type: 'GET',
  dataType: 'jsonp'
}).then((weatherConditions) => {
  $.ajax({
    url: 'https://api.recipes.com/'+ weatherConditions,
    type: 'GET',
    dataType: 'jsonp'
  }).then((data) => {
    $.ajax({
      url: 'api.github.com/user/hackeryou',
      type: 'GET',
      dataType: 'jsonp'
    }).then((data) => {
      $.ajax({
        url: 'developers.facebook.com/api/',
        type: 'GET',
        dataType: 'jsonp'
      }).then((data) => {
        // more AJAX calls
      });
    });
  });
});
```
Chaining functions like this (i.e. so that they are executed from top to bottom in a file), is lovingly referred to as [callback hell](http://callbackhell.com).

## Promises

Rather than putting our AJAX calls (or any code) into callback after callback, we can queue up what's called a _promise_. A promise [is an object that represents the eventual completion or failure of an asynchronous event](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise). 

You can think of a JavaScript promise like a regular, real-life promise. If your best friend promises to get you a birthday gift, you can reasonably expect that on your birthday: ✨🎁✨ . It's not your birthday **yet** so they haven't made you a gift **right now**, but by the end of the day on your birthday, you will know if they've done what they promised. 

A _fulfilled_ promise is one where your best friend gives you a gift (or you receive the data you expect from your API).
A _rejected_ promise is one where your best friend wasn't able to get you a gift (or you don't receive any data from your API).

To write a promise from scratch, you need three things:
  1. The `new` keyword
  1. A function that will run when the promise is fulfilled
  1. A function that will run when the promise is rejected

```js
// here we create the promise and name the functions we will run when the promise is filfulled or rejected
const myPromise = new Promise( (fulfill, reject) => {
  // here we say what will be returned from the promise if it is fulfilled
  fulfill('successful!')
  // here we say what will be returned from the promise if it is rejected
  reject('not successful!')
})
```

> Capital-P `Promise` is a special kind of object in JavaScript called a _prototype_ that you create a new copy of using the `new` keyword. Promises have some special stuff baked in, which is why you make a copy of the prototype when you want to use one. It's like opening up a preformatted resume in a word processor. More on this in [our lesson on class-based programming](https://github.com/HackerYou/bootcamp-notes/blob/master/applied-javascript/class-based-programming.md).

To invoke a promise, you need to let the browser know what happens when the data comes back using the `.then()` method:

```js
myPromise.then( (goodResult) => {
  // goodResult is a variable whose value is 
  // whatever we defined in the fulfill function when we created the promise
  console.log(goodResult);
}).catch(error => {
    // error is a variable whose value is 
    // whatever we defined in the reject function when we created the promise
    console.log(error)
})
```

Promises are supported in all modern browsers, but some older ones may require you to use a promise library; jQuery has one built into it. We're already very familiar with one function that returns a promise: the `$.ajax()` method!

Download [pokemon-promise-example.html](https://hychalknotes.s3.amazonaws.com/pokemon-promise-example.html).

You'll see that instead of using a success callback like this:

```js
$.ajax({
  url: 'https://www.weather.com/toronto',
  type: 'GET',
  dataType: 'jsonp'
}).then((data) => {
    console.log(data)
});
```
...we're **storing the AJAX request in a variable**. Doing so tells our code that we **promise** we won't try to  run the `.then()` function without knowing what the AJAX call returned. It's important to note that the variable **does not yet** contain the returned data.

```js
const pokemonApp = {};

pokemonApp.url = 'http://pokeapi.co/api/v2/pokemon/1/';

pokemonApp.getPokemon = $.ajax({
  url: 'pokemonApp.url',
  method: 'GET',
  dataType: 'JSON',
});
```
jQuery's `$.when()` method _listens_ for when a promise is either fulfilled or rejected. The JavaScript method `.then()` tells the browser what to do with the data returned from the promise.

```js
$.when(pokemonApp.getPokemon).then((caughtPokemon) => {
  console.log(caughtPokemon);
});
```
Because we only have one promise, can omit `$.when()` and write:

```js
const pokemonApp = {};
pokemonApp.url = 'http://pokeapi.co/api/v2/pokemon/1/';

pokemonApp.getPokemon = $.ajax({
  url: 'pokemonApp.url',
  method: 'GET',
  dataType: 'JSON',
});

pokemonApp.getPokemon.then((caughtPokemon) => {
  console.log(caughtPokemon);
});
```

### Listening for success and failure
Sometimes, APIs don't return the information we want. Right now we have no way to deal with that! We've only written callback functions that assume we have response data from the API. Luckily, the `.then()` method accepts **two** callback functions. We've been providing one that specifies what to do when the promise is fulfilled (i.e. _successful_). We can also provide one that says what to do when the promise is rejected (i.e. _fails_).

Here's an example of a `.then()` function with two callbacks: the first one (the fulfill callback) has a parameter called `caughtPokemon`, and the second one (the reject callback) takes the argument that's passed as the `err` parameter and logs it:
```js
$.when(pokemonApp.getPokemon)
  .then((caughtPokemon) => {
    console.log(caughtPokemon);
  }, function(err) {
    console.log(err);
  });
```

This works fine, but we can make our lives easier by using the JavaScript failure handler for promises: `.catch()`. However, because we are using jQuery, we need to use their specific implementation of the failure handler known as `fail()`:

```js
$.when(pokemonApp.pokemon)
  .then((caughtPokemon) => {
    console.log(caughtPokemon);
  })
  .fail((error) => {
    console.log(error);
  });
```

> Remember: if there is no semi-colon after a `)` and the next line starts with `.`, the JavaScript engine will assume you are **chaining** functions.

### Working with multiple promises

Imagine we want to catch two Pokémon and then console log the contents of the Poké ball that contains both of them **only when** they are both comfortably inside. (This was [heavily](https://bulbapedia.bulbagarden.net/wiki/Bag) [researched](https://bulbapedia.bulbagarden.net/wiki/Pok%C3%A9_Ball), don't argue about how they fit.)

```js
// create a variable to hold the first promise
pokemonApp.pokemonOne = $.ajax({
  url : 'http://pokeapi.co/api/v2/pokemon/1/',
  dataType : 'json',
  method: 'GET'
});

// create a variable to hold the second promise
pokemonApp.pokemonTwo = $.ajax({
  url : 'http://pokeapi.co/api/v2/pokemon/2/',
  dataType : 'json',
  method: 'GET'
});

// when we get BOTH pokemon (i.e. when BOTH promises are settled)
$.when(pokemonApp.pokemonOne, pokemonApp.pokemonTwo)
  // use the results of those promises
  .then((caughtPokemonOne, caughtPokemonTwo) => {
    // and show them to us
    console.log(caughtPokemonOne, caughtPokemonTwo);
  })
  // if we don't catch 'em all, show us an error
  .fail((err1, err2) => {
    console.log(err1, err2);
  });
```
We create promises called `pokemonApp.pokemonOne` and `pokemonApp.pokemonTwo` and pass them as a comma-separated list to the `$.when()` function. Once they are settled, we pass the returned data as arguments to the `.then()` function, which logs the data to the console.

#### Let's get a whole bunch of Pokémon
Let's get all the Pokémon from 1-40. We could write a function that takes a number as an argument and will make the request for that Pokémon:
```js
function getPokemon(number) {
  $.ajax({
    url : `https://pokeapi.co/api/v2/pokemon/${number}/`,
    dataType : 'json',
    method: 'GET'
  })
  .then((caughtPokemon) => {
    console.log(`${caughtPokemon.name} is Pokémon number ${caughtPokemon.id}`.);
  });
}
```

We can run a `for` loop that goes from 1-40 and calls `getPokemon(i)` passing in `i` for each iteration of the `for` loop:

```js
for(let i = 1; i <= 40; i++) {
  getPokemon(i);
}
```

But oh no! There is a problem! The output will probably look something like this: 

```bash
charmeleon is Pokémon number 5.
charmander is Pokémon number 4.
venusaur is Pokémon number 3.
rattata is Pokémon number 19.
nidoking is Pokémon number 34.
ekans is Pokémon number 23.
nidorino is Pokémon number 33.
beedrill is Pokémon number 15.
```

They are out of order! The problem here is that we are making a whole bunch of requests and since these are **asynchronous** calls, they are not guaranteed to come back in order.

### Making sure the order matters

How do we make sure we get the pocket monsters back in order? First let's change the `getPokemon` function to return an AJAX call using `$.ajax()` and remove the `.then()` method. 

> Making your function return an AJAX call is especially helpful when we need to make multiple API calls that depend on one another - similar to how we're making multiple calls to the Pokemon API and logging each Pokemon in the correct order. Remember that `$.ajax` returns a promise, so the return value of the function is a promise object. Most likely you will only need make your function return a promise when you want to queue up multiple promises.

```javascript
function getPokemon(number) {
  return $.ajax({
    url : `http://pokeapi.co/api/v2/pokemon/${number}/`,
    dataType : 'json',
    method: 'GET'
  });
}
```

Let's create a new empty array called `pokeBag` and then push our Pokémon into that array from inside the `for` loop.

```javascript
const pokeBag = [];

for(let i = 1; i <= 40; i++) {
  pokeBag.push(getPokemon(i));
}
```

Now the `pokeBag` variable holds an array of promises! **And** the order that we pushed the promises in will remain intact because: arrays! Aren't they swell? Now, no matter how long the promises take to settle, the array order will never change.

🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥

Okay, so, how do we get the data out of that array?

## Rest parameters

_Rest parameters_ allow us to gather the first, second, third, and all the **rest** of our **parameters** into a function!

Imagine you have a function that takes any number of arguments and returns the sum:
```js
add(2,3,4,5,6,7)
// 27
```
You'd probably end up writing a function that looks like this:
```js
const add = function() {
  const numbers = Array.prototype.slice.call(arguments);
  return numbers.reduce( (a,b) => a + b );
};
```

Whattttttt in the world does `Array.prototype.slice.call(arguments)` mean?! `arguments` is an **array-like object** (not an actual array) that is accessible on all functions. 

Check this out in the console:
```js
const add = function() {
  console.log(arguments)
};
// add(1,2,3)
// Arguments(3) [1, 2, 3, callee: ƒ, Symbol(Symbol.iterator): ƒ]
```
We can, however, use the `arguments` object to create an **actual** array!

The `arguments` object, like all objects in JavaScript (and everything in JavaScript is an object!), has a parent object from which it inherits its methods (via the `.prototype` property). Arrays made from the Array prototype have the `.slice()` method. So, `Array.prototype.slice`. We can use `.slice()` to create an actual array from our `arguments` value. Using `.call`, we can use the `.slice` method with `arguments` as the context to create an array...

...that we can [use `.reduce` on](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)!

😅It's a lot!😅

Rest parameters make that whole thing much faster! Using the syntax `...` before the name of the variable that is an array-like object of values, you can turn whatever the `arguments` of the function are into an actual array!

```js
const add = function(...numbers) {
  return numbers.reduce( (a,b) => a + b );
};
add(2,3,4,5,6,7);
// 27
```

For our Pokémon example, we can use rest parameters to tell our browser that we want to run the `.then()` function with each of the responses from the promises held in the `pokeBag` passed in.

```javascript
$.when(pokeBag)
  .then((...args) => {
    console.log(args);
  });
```

But wait! `pokeBag` is an **array of promises!** Promises are not values, they are only the promise of a future value! This means we have to listen to **each** item in the array. 

How do we listen? With `$.when()`!
How do we get `$.when()` to listen to each promises? With the spread operator!

> Note that arrow functions don't have an arguments object the same way that function expressions and declarations do. For more about that, [check out MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions#No_binding_of_arguments).

## Spread operator
The _spread operator_ allows us to pass an array of arguments into a function as if we were doing it manually one-by-one. 

Imagine you wanted to find the highest of the numbers in an array using `Math.max`:
```js
const numbers = [39,25,90,123];
const max = Math.max(numbers);
console.log(max); // NaN
```

You can't! `Math.max` is a method that accepts a comma separated list of values returns the max. It doesn't know what to do when we pass it an array. In the old days, the way get around this was a method called `.apply` that takes an array and calls a function on each item in the array.

```js
const numbers = [39,25,90,123];
const max = Math.max.apply(null,numbers);
console.log(max); // 123
```
Like rest parameters, the spread operator is also denoted by `...`.

```js
const numbers = [39,25,90,123];
const max = Math.max(...numbers);
console.log(max); // 123
```

The difference between the spread operator and rest parameters is the difference between parameters and arguments. You use one to talk about the placeholders in a function (parameters/rest parameters) and you use one to talk about the actual values passed to a function (arguments/spread operator). 

Using the spread operator  we can take an array of promises and pass it to `$.when()`. We are saying, "Please do this function for every single item in the array." Then, using rest parameters, we can gather all the arguments passed to the `.then()` method into an array.

```javascript
$.when(...pokeBag)
  .then((...args) => {
    console.log(args);
    args.forEach((poke,i) => console.log(poke[0].name,poke[0].id));
  });
```

This will allow us to take all the data and do something with it! One thing to think about with the `$.when` method is that when it is given more than one promise it will give you each bit of data as an array. So now we have an array of arrays, or a _multi-dimensional array_. It will look something like this:

```javascript
[
  [DataObject, Status, Original_Promise],
  [DataObject, Status, Original_Promise],
  [DataObject, Status, Original_Promise]
]
```

We just want that `DataObject`, so let's make one last change to the code above so it only gives us the thing we want:

```javascript
$.when(...pokeBag)
  .then((...args) => {
    args = args.map(pokemon => 
      console.log(pokemon[0])
    );
  });
```

Now we just have an array of the data we want! 😚👌 

> `$.when()` and `.then()` are great tools, but make sure you're using them correctly! Don't use them in place of a regular callback function.

## Syntactic sugar: `async` and `await`

New to ES2017 are the keywords `async` and `await`. These keywords allow us to work with any promise synchronously.

Let's look at an example:

```js
const getPokemon = (id) => {
  return $.ajax({
    url: `https://pokeapi.co/api/v2/pokemon/${id}`,
    method: 'GET',
    dataType: 'json'
  });
};

const getType = (name) => {
  return $.ajax({
    url: `https://pokeapi.co/api/v2/type/${name}`,
    method: 'GET',
    dataType: 'json'
  });
};

async function getData() {
  const firstPokemon = await getPokemon(1);
  const type = await getType(firstPokemon.types[0].type.name);

  console.log(type);
};

getData();
``` 

In this example we have two functions that make AJAX requests and, more importantly, that both return promises. In order to use `async` or `await` we need to first define a function as being `async`.

```js
async function getData() {

};
```

Once we do that, we are able to use the `await` keyword inside of that function. Once the `async` function hits the `await` keyword, it will stop and wait till the promise on the right side of the keyword is settled. When it is settled, it will provide the value to the variable on the left. 

```js
const firstPokemon = await getPokemon(1);    
const type = await getType(firstPokemon.types[0].type.name);
```

This is another way to structure your code when you need to get one bit of information from somewhere and use it in another function. 

## Resources
* If you are working with an unknown number of promises, this pattern still works but we need to change it slightly. Check out this [video](https://www.youtube.com/watch?v=Y2a0Xv3giho) for a full code-along doing just that! 
* Here's a [video](https://youtu.be/j2DMwUYEC88?list=PL57atfCFqj2h5fpdZD-doGEIs0NZxeJTX) on the spread operator and rest parameters. 
* Here's a [video](https://youtu.be/j2DMwUYEC88?list=PL57atfCFqj2h5fpdZD-doGEIs0NZxeJTX) about a bunch of things you can do with the spread operator.
* Here's a [talk](https://www.youtube.com/watch?v=9YkUCxvaLEk) on async and await by instructor Wes Bos. 
* Here's a nice flowchart from MDN showing life of a promise.
  ![Diagram of the life of a JavaScript promise](https://user-images.githubusercontent.com/8013918/51422191-6bcaf780-1b78-11e9-8dd0-bd8d7b19fae9.png)

## Exercises

### Spread and rest
Looking for more practice with spread and rest? Download [spread-rest-exercises.zip](https://hychalknotes.s3.amazonaws.com/spread-rest-exercises.zip) to get started. Feel free to tackle these on your own time. There's an answer key included in case you get stuck! 

### Promise challenge
Download [hp-promise-bootcamp-challenge.zip](https://hychalknotes.s3.amazonaws.com/hp-promises-bootcamp-challenge.zip) to get started. Feel free to tackle this one on your own time. There's an answer key included in case you get stuck! For this challenge, we want to display the names of Gryffindor members on the page.