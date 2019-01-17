<!-- Student takeaway -->
<!-- By the end of this lesson, the student should know:
- 
-->
# Working with asynchronous events
## Promises
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
    }).then((data)  => {
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

Rather than putting our AJAX calls (or any code) into callback after callback, we can queue up what's called a _promise_. A promise [is an object that represents the eventual completion or failure of an asynchronous event](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise). 

You can think of a JavaScript promise like a regular, real-life promise. If your best friend promises to get you a birthday gift, you can reasonably expect that on your birthday: ✨🎁✨ . It's not your birthday **yet** so they haven't made (or bought) you a gift **right now**, but by the end of the day on your birthday, you will know if they've done what they promised. 

A _fulfilled_ promise is one where your best friend gives you a gift (or you receive the data you expect from your API).
A _rejected_ promise is one where your best friend wasn't able to get you a gift (or you don't receive any data from your API).

Promises are supported in all modern but some older ones may require you to use a promise library - jQuery has one built into it, so we'll use that.

For an example of a single promise, open [pokemon-promise-example.html](https://hychalknotes.s3.amazonaws.com/pokemon-promise-example.html).

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
...we're **storing the AJAX request in a variable**. Doing so tells our code that we **promise** to have information back from that AJAX request when we run the `.then()` function. It's important to note that the variable **does not yet** contain the returned data.

```js
let pokemonApp = {};
pokemonApp.url = 'http://pokeapi.co/api/v2/pokemon/1/';

// storing the AJAX request in a variable creates a promise 
pokemonApp.getPokemon = $.ajax({
  url: 'pokemonApp.url',
  method: 'GET',
  dataType: 'JSON',
});
```
jQuery's `$.when()` method _listens_ for when this promise is either fulfilled or rejected. The JavaScript method `.then()` tells the browser what to do with the data returned from the promise.

```js
$.when(pokemonApp.getPokemon).then((caughtPokemon)  => {
  console.log(caughtPokemon);
});
```
Because we only have one promise, can omit the `$.when()` and write:
```js
let pokemonApp = {};
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

Here's an example of a `.then()` function with two callbacks: the second one takes the parameter `err` and logs it:
```js
$.when(pokemonApp.getPokemon).then((caughtPokemon) => {
  console.log(caughtPokemon);
}, function(err) {
  console.log(err);
});
```
This works fine, but we can make our lives easier by naming the function:
```js
$.when(pokemonApp.pokemon).then((caughtPokemon) => {
  console.log(caughtPokemon);
}).fail((error) => {
	console.log(error);
});
```
Here we use `.then()` to handle the promise's fulfilled response. We also chain `.fail()` to handle the response if it's an error.

Sometimes you'll see these callback functions indented like this for ease of reading:
```js
$.when(pokemonApp.getPokemon)
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
// create a promise to get the first pokemon
pokemonApp.pokemonOne = $.ajax({
  url : 'http://pokeapi.co/api/v2/pokemon/1/',
  dataType : 'json',
  method: 'GET'
});

// create a promise to get the second pokemon
pokemonApp.pokemonTwo = $.ajax({
  url : 'http://pokeapi.co/api/v2/pokemon/2/',
  dataType : 'json',
  method: 'GET'
});

// when we get BOTH pokemon
$.when(pokemonApp.pokemonOne, pokemonApp.pokemonTwo)
  // use the results of those promises
  .then((caughtPokemonOne, caughtPokemonTwo) => {
    // and show them to us
   console.log(caughtPokemonOne, caughtPokemonTwo);
  })
 // if we don't catch any, show us an error
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

BUT!! There is a problem! The output will probably look something like this: 

```bash
bulbasaur is Pokémon number 1.
venusaur is Pokémon number 3.
charmander is Pokémon number 4.
ivysaur is Pokémon number 2.
charmeleon is Pokémon number 5.
```

They are out of order! The problem here is that we are making a whole bunch of requests, but since these are asynchronous calls the order at which they come back is not guaranteed.

### Making sure the order matters

So if we have a whole bunch of calls working, but we are getting them out of order, how can ensure everything comes back in order? Let's change our code a bit. First let's change the `getPokemon` function to return a call to `$.ajax`, and we will leave off the `.then` method. Remember that `$.ajax` returns a Promise, so the return value of the function is a Promise object.

```javascript
function getPokemon(number) {
  return $.ajax({
    url : `http://pokeapi.co/api/v2/pokemon/${number}/`,
    dataType : 'json',
    method: 'GET'
  });
}
```

Let's create a new variable called `pokemon` that is an empty array, and then use that to push our pokemon in from inside the `for` loop.

```javascript
const pokemon = [];

for(let i = 1; i <= 40; i++) {
  pokemon.push(getPokemon(i));
}
```

Now the `pokemon` variable holds an array of promises, the important thing here is that the order that we push them in is still intact. Even though some of them might take longer to settle, or come back than others, the array order will never change.

Good, good, great, right? But how do we get that data?! 

## Spread Operator

Some times you want to do something with an array that we can't! For example let's assume we have an array of numbers that we want to find the max of.

```js
let numbers = [39,25,90,123];
let max = Math.max(numbers);
console.log(max); // NaN
```

`Math.max` is a method that accepts a comma separated list of values and will return the max! Sadly we can not pass an array to it. There is a way to get around this, we can use a method called `.apply` that will take an array and call a function as if we had passed them in as a list.

```js
let numbers = [39,25,90,123];
let max = Math.max.apply(null,numbers);
console.log(max); // 123
```

This could be a little confusing, what if there was an easier way to do this? In ES6 there is a the spread operator! The syntax looks like this `...numbers`, what this does is spread out the elements from the array! So we can change the above `.apply` call to look like this.

```js
let numbers = [39,25,90,123];
let max = Math.max(...numbers);
console.log(max); // 123
```

#### Using spread to concat

You can use the spread operator to also concatenate arrays together!

```js
let numbersArray1 = [3,4,5,7,8];
let numbersArray2 = [9,6,10,11];
let concatArray = [...numbersArray1,...numbersArray2];
console.log(concatArray); // [3, 4, 5, 7, 8, 9, 6, 10, 11]
```

There is a lot more you can do with the spread operator, to find out more check out this <a href="https://youtu.be/j2DMwUYEC88?list=PL57atfCFqj2h5fpdZD-doGEIs0NZxeJTX" target="_blank">video!</a> 

## Rest Parameters

The spread operator allows us to pass an array of arguments into a function. On the flip side rest parameters allows us to gather the parameters in our function! Just like the spread operator the rest parameter syntax also involves the `...` at the beginning of the variable name.

Let's look at an example of where this would come into play. Imagine we have a function that takes any number of arguments and return the sum, `add(2,3,4,5,6,7)` would return 27.

```js
let add = function() {
	let numbers = Array.prototype.slice.call(arguments);
	return numbers.reduce( (a,b) => a + b );
};
add(2,3,4,5,6,7);
```

What in the world does `Array.prototype.slice.call(arguments)` mean?! First things first is this `arguments` keyword. `arguments` is an Array LIKE object, meaning it is not an actual array, that is a collection of the arguments passed to a function. We can use this to create an actual array we can use `.reduce` on.

If you remember, everything in JavaScript is an object. All of these objects have a parent object that they inherit their methods from, they do this via a `.prototype` property. Array's have the `.slice` method that we can use to create an actual array from our `arguments` value. Using `.call` we can call the `.slice` method with `arguments` as the context to create an array....whoa that is a lot. 

## Enter rest parameters!

```js
let add = function(...numbers) {
	return numbers.reduce( (a,b) => a + b );
};
add(2,3,4,5,6,7);
```

WOW! That was a lot easier. Rest parameters creates an actual array from the arguments passed to a function, so we can use methods like `.reduce` on it!

If you want to learn a little more, check out this <a href="https://youtu.be/j2DMwUYEC88?list=PL57atfCFqj2h5fpdZD-doGEIs0NZxeJTX" target="_blank">video</a> on the spread operator and rest parameters. 




Using the spread operator `...` we can take this array of promises and pass it to `$.when` as if we did it manually one after the other. Then using rest parameters, `...`(same syntax as spread, just different use), we can gather all the arguments passed to the `.then` method into an array.

```javascript
$.when(...pokemon)
  .then((...args) => {
    console.log(args);
    args.forEach((poke,i) => console.log(poke[0].name,poke[0].id));
  });
```

This will allow us to take all the data and do something with it! One thing to think about with the `$.when` method is that it will, when given more than one promise, give you each bit of data as an array. So now we have an array of arrays, or a multi dimensional array. It looks something like this.

```javascript
[
  [DataObject, Status, Original_Promise],
  [DataObject, Status, Original_Promise],
  [DataObject, Status, Original_Promise]
]
```

We just want that `DataObject`, so lets make one last change to the code above to give us JUST what we want.

```javascript
$.when(...pokemon)
  .then((...args) => {
    args = args.map(data => data[0]);
  });
```

Now we just have an array of the data! 😚👌 

## Working with an unknown number of promises

If you are looking to have to work with an unknown number of promises, this pattern still works. However we need to change it slightly, and some magic methods need to be used. Check out this [video](https://www.youtube.com/watch?v=Y2a0Xv3giho) for a full code along doing just that! 

## Async await

New to ES2017 is a new way to deal with asynchronous events. Using the `async` and `await` keywords we can work with any Promise in a synchronous manner. Let's look at an example.

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

In this example we have two functions that make AJAX requests, more importantly, they both return Promises. In order to use `async`/`await` we need to first define a function as being `async`.

```js
async function getData() {

};
```

Once we do that we are able to use `await` keyword inside of it. Once the `async` function hits the `await` keyword, it will stop and wait till the promise on the right side of the keyword is settled. When it is settled, it will provide the value to the variable on the left. 

```js
const firstPokemon = await getPokemon(1);    
const type = await getType(firstPokemon.types[0].type.name);
```

This is a very helpful technique for when you need to get one bit of information from something and use it in another function. 