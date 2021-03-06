# What is next in JavaScript

## Map & Set
New to JavaScript in the ES6 update (ES2015) were two new data structures: `Map` and `Set`.

## Map
A `Map` is an object that is a group of key/value pairs. However there are a few important differences between a `Map` and a regular object. 

A `Map` can have any value as a key, this means it could have a function as a key! Another important difference is that the insertion order of properties is maintained. (Remember that for regular objects the properties' order is NOT guaranteed.)

### Creating a Map
In order to create a Map, we need to use its built-in constructor. Creating a Map looks something like this:

```js
const myMap = new Map();
``` 

You might notice the `new` keyword here. The `new` keyword is used when we want to create a new instance of something. `Map` is what we call a *constructor*. A constructor is a type of object that is used to create many instances of itself. We will learn more about this when we talk about classes, but just know for now that this is a very common pattern.

### Adding to our Map
In order to add properties to our `Map` we use the `.set()` method. 

```js
myMap.set('key','value');
```

### Getting a property
Getting a property from a `Map` is very similar. We use the `.get()` method to retrieve values from a property.

```js
myMap.get('key'); //returns value
```

## Set
A `Set` is similar to a `Map`, in that we need to construct it using the `new` keyword. However there is one major difference is that a `Set` is just a list of elements, similar to an array.

```js
const cities = new Set();
```

### Adding to a Set
Similar to a `Map` we have to use a method to add to a `Set`. In this case we use the `.add()` method.

```js
cites.add('Toronto');
```

### Retrieving a property from a Set 
Unlike a `Map` we don't have a `.get()` method. However we have a `.has()` method that can be used to check to see if something exists in the `Set`.

```js
cities.has('Toronto'); //true
```

### Unique elements in a Set
One of the really cool features of a `Set` is that it CANNOT contain duplicate elements. Let's look at an example!

```js
const cities = ['Toronto','Montreal','Oakville','Toronto','Ottawa'];

const uniqueCities = new Set(cities);
```

This `Set` will not remove any extra "Toronto" elements

### Iterating through Maps and Sets
`Map` and `Set` have some shared methods for iterating through them.

They both have the `.forEach()` method that we are used to, which works exactly like it does for arrays.

#### .entries(), .values()
Some methods to look at that might be less intuitive are `.entries()` and `.values()`. These methods return what is called an *iterable object*.

These methods are used inside of a `for...of` loop. This is a new form of the `for` statement. The `for...of` statement looks similar to a `for...in` loop, but there is one key difference: they only work for iterable objects.

```js
const cities = ['Toronto','Montreal','Oakville','Toronto','Ottawa'];

const uniqueCities = new Set(cities);

for(let value of uniqueCities.values()) {
  console.log(value);
}
```

What is an iterable object? It is an object in JavaScript that implements a `.next()` method.

```js
const cities = ['Toronto','Montreal','Oakville','Toronto','Ottawa'];

const uniqueCities = new Set(cities);
const cityIterator = uniqueCities.values();
console.log(cityIterator.next()); 
/*
{
    done: false,
    value: "Toronto"
}
*/
```

The `.entries()` method it is a bit different, so it will return a slightly different value.

```js
const person = new Map();
person.set('name', 'Susan Smith');
person.set('age', 25);

for(let [key,value] of person.entries()) {
  console.log(key,value);
}

// name Susan Smith
// age 25
```

The parameters `key` and `value` can be anything we want. The order is the only thing that is important here. 

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
  // ...
};
```

Once we do that we are able to use `await` keyword inside of it. Once the `async` function hits the `await` keyword, it will stop and wait till the Promise on the right side of the keyword resolves. Once it resolves it will provide the value to the variable on the left. 

```js
const firstPokemon = await getPokemon(1);    
const type = await getType(firstPokemon.types[0].type.name);
```

This is a very helpful technique for when you need to get one bit of information from something and use it in another function. 

## Additional Resources
* [Async + Await in JavaScript, talk from Wes Bos](https://www.youtube.com/watch?v=DwQJ_NPQWWo)