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
Let's say we're building an app that plans an average, boring day for you. It makes two AJAX requests - one for the weather, and one for recipes to make for dinner. We need both requests to finish before we print the information to the page.

We **could** run the first AJAX request and put the second AJAX request in its callback, so that the second AJAX request runs when the first one is done. Then we can pass all the collected data on to a function that will print our info to the page. That would look like this:

```js
$.ajax({
  url: 'https://www.weather.com/toronto',
  type: 'GET',
  dataType: 'jsonp'
}).then((weatherConditions) => {
  $.ajax({
    url: 'https://api.recipes.com/category/boring',
    type: 'GET',
    dataType: 'jsonp'
  }).then((recipes) => {
    emptyLifeApp.printToPage(weatherConditions, recipes);
  });
});
```

This isn't ideal because we need to wait for the response from `https://www.weather.com/toronto` to come back before we can make a call to `https://api.recipes.com/`, which slows things down; it would be faster if we could send all the calls out at the same time so that they all complete as soon as possible. Also, what if we had to complete 10 API calls in sequence?  

Something like this:

```js
$.ajax({
  url: 'https://www.weather.com/toronto',
  type: 'GET',
  dataType: 'jsonp'
}).then((weatherConditions) => {
  $.ajax({
    url: 'https://api.recipes.com/category/boring',
    type: 'GET',
    dataType: 'jsonp'
  }).then((recipes) => {
    $.ajax({
      url: 'https://api.televisionArchive.com/shows/daytimeShopping',
      type: 'GET',
      dataType: 'jsonp'
    }).then((TVguide) => {
      $.ajax({
        url: 'https://developers.paintAndHardware.com/paintDryingTimes',
        type: 'GET',
        dataType: 'jsonp'
      }).then((watchTime) => {
        // more AJAX calls
          .then(() => {
            // and more AJAX calls
            .then(() => {
              // and more and more and more
              .then(() => {
                // never-ending AJAX calls
                .then(() => {
                  // there is no more Juno, there is only AJAX calls
                })
              })
            })
          })
      });
    });
  });
});
```

Chaining functions like this (i.e. so that they are executed from top to bottom in a file), is lovingly referred to as [callback hell](http://callbackhell.com).


## Promises

Rather than putting our AJAX calls (or any code) into callback after callback, we can queue up what's called a _promise_. A promise [is an object that represents the eventual completion or failure of an asynchronous event](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise). 

You can think of a JavaScript promise like a regular, real-life promise. If your best friend promises to make you special a birthday gift, you can reasonably expect to receive that present on your birthday: ✨🎁✨ . It's not your birthday **yet** so they haven't made you a gift **right now**, but by the end of the day on your birthday, you will know if they've done what they promised. 

A _fulfilled_ promise is one where your best friend gives you a gift (ie. you receive the data you expect from your API).
A _rejected_ promise is one where your best friend wasn't able to get you a gift (ie. you don't receive any data from your API).

To write a promise from scratch, you need three things:
  1. The `new` keyword
  1. A function that will run when the promise is fulfilled (promise kept)
  1. A function that will run when the promise is rejected (promise broken)

```js
// here we create the promise and name the functions we will run when the promise is fulfilled or rejected
const myPromise = new Promise( (fulfill, reject) => {

  // here we say what will be returned from the promise if it is fulfilled
  fulfill('successful!')

  // here we say what will be returned from the promise if it is rejected
  reject('not successful!')
})
```

> Capital-P `Promise` is a special kind of object in JavaScript called a _prototype_. When you use invoke the prototype along with the `new` keyword, you create a new copy, or _instance_ of the prototype.
>
> Promises have some special stuff baked in, which is why you make a copy of the prototype when you want to use one. It's like opening up a preformatted resume in a word processor. More on this in [our lesson on class-based programming](https://github.com/HackerYou/bootcamp-notes/blob/master/applied-javascript/class-based-programming.md).

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

So, the general idea is like this:
* We use `new Promise` to create and name a promise, and to define what should be returned if it is fulfilled, and what should be returned if it is rejected.
* We access the returns using methods built into the promise object, `.then()` (when it is fulfilled) and `.catch()` (when it is rejected).
* Each of the above methods takes a callback. Those callbacks are automatically passed the return from their respective promise outcomes (like we've already seen with `$.ajax` passing data to `.then()`):
  * `.then( (fulfillReturn) => {} );`
  * `.catch( (rejectReturn) => {} );`

That's the abstract, but it helps to see it in practice. Let's create a new HTML file with some `<script>` tags and write our own promise from scratch.

First we create a variable. In our promise, we will be "waiting" to see if it is true or false:

```js
const isTherePupHere = true;
```

Next, we use the `new` keyword to build a promise called `lookForFloof`. Inside our promise, we can use an if-statement to check the value of our variable. This is a bit like waiting to hear the result of an AJAX call - did we get a 200 back (ie. `isTherePupHere === true`)? Or did we get an error (ie. `isTherePupHere === false`)? 

```js
const lookForFloof = new Promise( () => {
  
  if (isTherePupHere) {
    // Do some stuff if the variable is true
  } else {
    // Do some stuff if the variable is false
  }

});
```

Once we know, we will want to do something (run a function!) if the promise succeeds or if it fails. The callback that we pass the `Promise` constructor takes two parameters - the names of the success and failure functions that will run in either case. These two functions themselves are defined behind the scenes by the constructor, we do not need to create them in our code:

```js
const lookForFloof = new Promise( (fulfill, reject) => {
  
  if (isTherePupHere) {
    fulfill(`Pet ittttttttttttt`);
  } else {
    reject(`Let's go to the park`);
  }

});
```

The argument passed to the fulfill and reject functions are what will be returned in each circumstance (in this case, if the variable is true then we get back a string of "Pet ittttttttttttt", and if it is false, we get back a string of "Let's go to the park").

Our new promise is ready to go. Let's log `lookForFloof` out, just to see that it is returning a promise object.

```js
console.log(lookForFloof);
```

Now to put it into use. Let's define a function which will call our promise, and decide what to do with the return. Our promise object has some built-in methods that we can use:

```js
const promiseMePups = () => {
  lookForFloof.then().catch();
}
```

If the promise resolves (which in this case means the variable is true), then the return from the fulfill function (in this case, our "Pet ittttttttttttt" string) is passed as an argument to the callback of the `.then()` method. If the promise is rejected (the variable is false), then the return from the reject function is passed as an argument to the callback of the `.catch()` method.

We name a parameter in each case, so that we can define what to do with each of the returns:

```js
const promiseMePups = () => {
  lookForFloof
    .then( (yeh) => {
      console.log(yeh);
    })
    .catch( (nah) => {
      console.log(nah);
    });
}
```

So, in this case, `yeh` will be `"Pet ittttttttttttt"` and `nah` will be `"Let's go to the park"`.

Let's call our function! Try it out, then go up and change the value of isTherePupHere to false, and reload the page to see the promise be rejected.

```js
promiseMePups();
```


## Using promises in the real world

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

pokemonApp.url = 'https://pokeapi.co/api/v2/pokemon/1/';

pokemonApp.getPokemon = $.ajax({
  url: 'pokemonApp.url',
  method: 'GET',
  dataType: 'JSON',
});
```
The JavaScript method `.then()` tells the browser what to do with the data returned from the promise.

```js
const pokemonApp = {};
pokemonApp.url = 'https://pokeapi.co/api/v2/pokemon/1/';

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
pokemonApp.getPokemon
  .then((caughtPokemon) => {
    console.log(caughtPokemon);
  }, (err) => {
    console.log(err);
  });
```

This works fine, but we can make our lives easier by using the JavaScript failure handler for promises: `.catch()`. However, because we are using jQuery, we need to use their specific implementation of the failure handler known as `fail()`:

```js
pokemonApp.pokemon
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
  url : 'https://pokeapi.co/api/v2/pokemon/1/',
  dataType : 'json',
  method: 'GET'
});

// create a variable to hold the second promise
pokemonApp.pokemonTwo = $.ajax({
  url : 'https://pokeapi.co/api/v2/pokemon/2/',
  dataType : 'json',
  method: 'GET'
});
```

The jQuery $.when() method is helpful when we are listening for the fulfillment or rejection of multiple promises:

```js
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
    console.log(`${caughtPokemon.name} is Pokémon number ${caughtPokemon.id}.`);
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
    url : `https://pokeapi.co/api/v2/pokemon/${number}/`,
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

Now the `pokeBag` variable holds an array of promises! **And** the order that we pushed the promises in will remain intact because - arrays! Aren't they swell? Now, no matter how long the promises take to settle, the array order will never change.

🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥🔥

Okay, so, how do we get the data out of that array?

We know that we want to use `$.when()` to listen for the fulfillment of the many promises in our `pokeBag`, and once they have successfully returned, we want to pass the results to our `.then()` method. So, our code will look something like this:

```javascript
$.when(pokeBag)
  .then((fulfilledPokes) => {
    console.log(fulfilledPokes);
  });
```

When we try this code out though, we're just getting an array full of objects. If we open one of the objects up, we see that it has some properties in it, a bunch of which are methods like `.complete()`, `.fail()`, `.then()`... that's a promise object! The array we're looking at is still just our original `pokeBag` array of promises.

There are two problems here for us to work through though:

* `pokeBag` is an array of promises (not values). The array as a whole **is** a value though. When we pass that array to `$.when()`, it believes that the array itself is the result we're waiting for and passes it along as-is to `.then()`. To fix this, we need to give `$.when()` access to each of the individual promises inside our array.
* Once we have the successful results, `$.when()` will pass them as individual arguments to the `.then()` method. Now we have the opposite problem - a large set of individual results that we want to work with as a whole (say, by iterating over them). We will need to collect the results together again inside our `.then()`, back into a new array.

So, we need to separate items out of an array to pass them as separate arguments, and then we will need to gather all the individual arguments passed to a function up into a new array. To do each of these, we can use the [spread operator](https://github.com/HackerYou/bootcamp-notes/blob/master/applied-javascript/js-superpowers-spread-rest-and-destructuring.md#spread-operator), then [rest parameters](https://github.com/HackerYou/bootcamp-notes/blob/master/applied-javascript/js-superpowers-spread-rest-and-destructuring.md#rest-parameters).


### Spread and rest

To give `$.when()` access to each of the individual promise objects inside our `pokeBag` array, we will use the spread operator, which allows us to use its `...` syntax to pass an array of arguments into a function as if we were doing it manually one-by-one.

We wrote this code:

```javascript
$.when(pokeBag)
  .then((fulfilledPokes) => {
    console.log(fulfilledPokes);
  });
```

However, rather than

`$.when( [PROMISE, PROMISE, PROMISE, PROMISE, (etc)] )`

our JS reads it like

`$.when( [AN ARRAY! THIS IS ALREADY A RETURNED VALUE, NOTHING TO WAIT FOR HERE!] )`

Instead, we will spread those promises out:

```javascript
/// The three dots before 'pokeBag' are the spread operator separating the values out of our array
$.when(...pokeBag)
  .then((fulfilledPokes) => {
    console.log(fulfilledPokes);
  });
```

Now, our JS sees

`$.when( PROMISE, PROMISE, PROMISE, PROMISE, (etc) )`

which is the correct syntax. `$.when()` will now wait until each of the individual promises are settled, and if they are it will then pass the return from each to `.then()`.

We will want to tell our `.then()` what to do with the results of our many promises (ie. the results of our API calls), but to write our parameters out in this case (both in the parentheses and then in the function itself) would be arduous, messy and very long, like:

```javascript
$.when(...pokeBag)
  .then((pokeResult01, pokeResult02, pokeResult03, pokeResult04, pokeResult05, pokeResult06, pokeResult07, pokeResult08, pokeResult09, pokeResult10, pokeResult11 .....etc. etc.) => {
    // We never even get to here because we die of fatigue while typing our parameters.
  });
```

Moreover, this means that we then have to write out the use of each of our results one-by-one, and if we change the number of promises then we have to also manually change the parameters. To make this shorter and more dynamic, we can use rest parameters, which similarly uses the `...` syntax, but this time to gather the first, second, third and all the **rest** of our parameters, and store them in a array:

```javascript
$.when(...pokeBag)
  .then((...fulfilledPokes) => {
    console.log(fulfilledPokes);
  });
```


### Finishing up

Our `fulfilledPokes` array contains our successful API results, but also some other things; it is an array of arrays, or a _multi-dimensional array_. This is because if the `$.when` method is given more than one promise, it returns each as a three-item array - something like this:

```javascript
[
  [DataObject, Status, Original_Promise],
  [DataObject, Status, Original_Promise],
  [DataObject, Status, Original_Promise]
]
```

We just want that `DataObject`, since that's the successful result of our API call. We can map over `fulfilledPokes` so it only gives us the thing we want:

```javascript
$.when(...pokeBag)
  .then((...fulfilledPokes) => {
    justTheGoodStuff = fulfilledPokes.map(pokemon => {
      return pokemon[0];
    });
    console.log(justTheGoodStuff);
  });
```

Now we just have an array of the data we want. Let's print out all 40 of our Pokemon, in order:

```javascript
$.when(...pokeBag)
  .then((...fulfilledPokes) => {
    justTheGoodStuff = fulfilledPokes.map(pokemon => {
      return pokemon[0];
    });
    
    justTheGoodStuff.forEach( (pokemon) => {
      console.log(`${pokemon.name} is Pokémon number ${pokemon.id}.`);
    });
  });
```

Incredible! 😚👌

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