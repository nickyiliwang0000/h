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

#### Enter rest parameters!

```js
let add = function(...numbers) {
	return numbers.reduce( (a,b) => a + b );
};
add(2,3,4,5,6,7);
```

WOW! That was a lot easier. Rest parameters creates an actual array from the arguments passed to a function, so we can use methods like `.reduce` on it!

If you want to learn a little more, check out this <a href="https://youtu.be/j2DMwUYEC88?list=PL57atfCFqj2h5fpdZD-doGEIs0NZxeJTX" target="_blank">video</a> on the spread operator and rest parameters. 

## Promises

Promises in JavaScript are a way to listen for something to be done - this is especially helpful when you are waiting for multiple Ajax requests to finish. 

Let's say we are are building an app that needs two Ajax requests: 1 for the Weather, and 1 for recipes. 

We could run the first one, and put the second one in the callback from the first, so it runs when the first is done:

```js
$.ajax({
    url: 'weather.com/toronto',
    type: 'GET',
    dataType: 'jsonp'
}).then((data) => {
    $.ajax({
        url: 'api.yummly.com',
        type: 'GET',
        dataType: 'jsonp'
    }).then((data)  => {
        // do something
    });
});
```

This, however, is not ideal because we need to wait for weather.com to come back before we get the recipes. Also, what if we had 10 requests that we needed to wait for before it came back? This is what is referred to as <http://callbackhell.com/>

```js
$.ajax({
    url: 'weather.com/toronto',
    type: 'GET',
    dataType: 'jsonp'
}).then((data) => {
    $.ajax({
        url: 'api.yummly.com',
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

So, rather than putting code into a callback, we "queue up" a promise, which sometime in the future will return the result.

Promises are in ES6(ECMAScript2015) and are just about 100% supported, but for the time being we can use any number of promise libraries - jQuery has one built it.

For an example of how to use a single promise, open <a href="https://hychalknotes.s3.amazonaws.com/promise-example1.html" class="exercise" download>promise-example1.html</a> 

You'll see that instead of using a success callback, we store the ajax request in a variable, this is called a _promise_. It's important to note that this **is not the data**, but a promise that data will eventually come back! Let's actually inspect that element by logging it to the console.

```js
let pokemonApp = {};
pokemonApp.getPokemon = $.ajax({
  url : 'http://pokeapi.co/api/v2/pokemon/1/',
  method: 'GET',
  dataType : 'JSON',
});
```

We can then _listen_ to that promise using `.when()`:

```js
$.when(pokemonApp.getPokemon).then((caughtPokemon)  => {
  console.log(caughtPokemon);
});
```
Note that when it is just one promise, the code above it just like this:

```js
let pokemonApp = {};
pokemonApp.getPokemon = $.ajax({
  url : 'http://pokeapi.co/api/v2/pokemon/1/',
  method: 'GET",
  dataType : 'JSON',
});

pokemonApp.getPokemon.then((caughtPokemon) => {
  console.log(caughtPokemon);
});
```

#### Listening for Success and Failures

API's can sometimes fail, and as it stands, we have no method of error handling. The `.then()` method accepts two callback functions to define what to do with our code. We previously provided one that was the success(resolve) callback, however, we can provide _another_ function that represents our fail(reject) callback.

```js
$.when(pokemonApp.getPokemon).then((caughtPokemon) => {
  console.log(caughtPokemon);
}, function(err) {
  console.log(err);
});
```

This syntax while it works, can get messy though. Instead we can use some more logically named methods to handle our success and failures.

If we use `.then()` to handle the success, we can then chain along `.fail()` to handle the errors.

```js
$.when(pokemonApp.pokemon).then((caughtPokemon) => {
  console.log(caughtPokemon);
}).fail((error) => {
	console.log(error);
});
```

Sometimes you'll see it indented like this - it's the same code just a little easier to read.

```js
$.when(pokemonApp.getPokemon)
  .then((caughtPokemon) => {
 	 console.log(caughtPokemon);
  })
  .fail((error) => {
    console.log(error);
  });
```

Remember, if there is no semi-colon and a `.` on the next line. The JavaScript engine will just think you are chaining along.

#### Multiple Promises

Now previously the only different between the above and the callback we have been using so far is syntax. However, it gets really handy when you need to wait for multiple APIs to return data, or if you need to wait for one set of data to return from an API so that you can make a second request to that API using some of the data you got back. 

It works the same way, except we pass `.when()` a comma separated list of promises. Once all have been fulfilled`.then` will fire the callback.


```js
pokemonApp.pokemonOne = $.ajax({
  url : 'http://pokeapi.co/api/v2/pokemon/1/',
  dataType : 'json',
  method: 'GET'
});

// create our second promise
pokemonApp.pokemonTwo = $.ajax({
  url : 'http://pokeapi.co/api/v2/pokemon/2/',
  dataType : 'json',
  method: 'GET'
});

$.when(pokemonApp.pokemonOne, pokemonApp.pokemonTwo)

  .then((caughtPokemonOne, caughtPokemonTwo) => {
   console.log(caughtPokemonOne, caughtPokemonTwo);
  })
 
  .fail((err1, err2) => {
    console.log(err1, err2);
  });
```

### A whole bunch of pokemon

Let's say that we want to get all the pokemon from 1-40, we could write a function that looks like this. It takes a `number` and will make the request for the pokemon of choice.

```javascript
function getPokemon(number) {
  $.ajax({
    url : `https://pokeapi.co/api/v2/pokemon/${number}/`,
    dataType : 'json',
    method: 'GET'
  })
  .then((pokemon) => {
    console.log(`${pokemon.name} is pokemon ${pokemon.id}`);
  });
}
```

We can run a `for` loop that goes from 1-40 and calls `getPokemon(i)` passing in `i` for each iteration of the `for` loop.

```javascript
for(let i = 1; i <= 40; i++) {
  getPokemon(i);
}
```

BUT!! There is a problem, the output will probably look something like this. 

```bash
bulbasaur is pokemon 1
venusaur is pokemon 3
charmander is pokemon 4
ivysaur is pokemon 2
charmeleon is pokemon 5
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

Now the `pokemon` variable holds an array of promises, the important thing here is that the order that we push them in is still intact. Even though some of them might take longer to resolve, or come back than others, the array order will never change.

Good, good, great, right? But how do we get that data?! Using the spread operator `...` we can take this array of promises and pass it to `$.when` as if we did it manually one after the other. Then using rest parameters, `...`(same syntax as spread, just different use), we can gather all the arguments passed to the `.then` method into an array.

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

### Working with an unknown number of promises

If you are looking to have to work with an unknown number of promises, this pattern still works. However we need to change it slightly, and some magic methods need to be used. Check out this [video](https://www.youtube.com/watch?v=Y2a0Xv3giho) for a full code along doing just that! 
