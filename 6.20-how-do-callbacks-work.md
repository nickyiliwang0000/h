In programming a *callback function* is a function that is used for something that might happen at a later point in time. In JavaScript this is most commonly used for events.

An example of this might be a click event with jQuery.

```js
$('div').on('click', function() {
	//Do some work in here
});
```

Here we set up an event using the `on` method. The `on` method takes two arguments here, the first is the event. In our case, the event is `click`. The second argument is what function we want to run when the click happens. *This function* is the callback function. 

When we provide the callback function to the `on` method, it has not run yet. The function is placed there as a value and only when we click the `div` will that function be called. 

Callback functions in JavaScript are functions that we are **passing as values** to other function or method calls.

So we could handle that above differently if we wanted.

```js
function handleClick() {
	//Do some stuff
}

$('div').on('click', handleClick);
```

Notice how we change the function passed to `on` and reference this new `handleClick` function. If we pass that into the method and do NOT use the `()`, we are passing the value of a function  inside of the `on` method. This function will be called when the click happens. 

## Making our own.

Let's explore this more by making our own function that accepts a callback. We will recreate the array `map` method, which is a method that takes a callback function and returns a new array based on it.

```js
function map(array, callback) {
	var results = [];
	for(var i = 0; i < array.length; i = i + 1) {
		var singleValue = array[i];
		results.push( callback(singleValue) );
	}
	return results;
}
```

We will break this down in a second, but let's see an example first:

```js
var numbers = [1,2,3,4,5];
var doubledNumbers = map(numbers, function(number) {
	return number * 2;
});

console.log(numbers); //[2,4,6,8,10]
```

So here we are creating an array called `numbers` and then creating a `doubledNumbers` variable. The `doubleNumbers` variable holds the returned result of our `map` function.

### How our map works

Here is `map` again for reference.

```js
function map(array, callback) {
	var results = [];
	for(var i = 0; i < array.length; i = i + 1) {
		var singleValue = array[i];
		results.push( callback(singleValue) );
	}
	return results;
}
```

Our `map` function has two parameters , an `array` parameter that will be what array we want to work with. Then it takes something called `callback`, and this will be our function. (Note that this parameter does NOT have to be called `callback` but we're using it here to help drive the point home.)

Inside of the `map` function, we create an empty `results` array that we will use to store our new data. Then we set up a `for` loop which will run for the length of the array passed to the function.

Each time we run the `for` loop, we push the returned value from calling `callback(singleValue)` into the `results` array. But what is the value of `callback`? Let's look again at the usage of `map`.

```js
var doubledNumbers = map(numbers, function(number) {
	return number * 2;
}); 
```

The value that is stored in `callback` is the function that takes the `number` parameter and returns `number * 2`. The parameter `number` is provided from our `map` function when we do this `callback(singleValue)`. The `singleValue` variable is the value that is being passed and assigned to the parameter for our callback. Since the `numbers` array is pretty small, let's walk through it one step at a time.

When we start the `map` function, this is what it looks like:

```js
function map(array, callback) {
	//array = [1,2,3,4,5];
	/*
	callback = function(number) {
		return number * 2;
	};
	*/
	var results = [];
	for(var i = 0; i < array.length; i = i + 1) {
		var singleValue = array[i];
		results.push( callback(singleValue) );
	}
	return results;
}
```

The first pass of the `for` loop will look like this:

```js
for(var i = 0; i < array.length; i = i + 1) {
	//i = 0;
	var singleValue = array[i]; //1
	//callback(singleValue) will be passing 1 as the value in singleValue
	//and since the function stored in callback will return number * 2,
	//the value being pushed into the results is going to be 2
	results.push( callback(singleValue) ); 
}
```

The second pass: 

```js
for(var i = 0; i < array.length; i = i + 1) {
	//i = 1;
	var singleValue = array[i]; //2
	//callback(singleValue) will be passing 2 as the value in singleValue
	//and since the function stored in callback will return number * 2,
	//the value being pushed into the results is going to be 4
	results.push( callback(singleValue) ); 
}
```

The third pass: 

```js
for(var i = 0; i < array.length; i = i + 1) {
	//i = 2;
	var singleValue = array[i]; //3
	//callback(singleValue) will be passing 3 as the value in singleValue
	//and since the function stored in callback will return number * 2,
	//the value being pushed into the results is going to be 6
	results.push( callback(singleValue) ); 
}
```

The fourth pass: 

```js
for(var i = 0; i < array.length; i = i + 1) {
	//i = 3;
	var singleValue = array[i]; //4
	//callback(singleValue) will be passing 4 as the value in singleValue
	//and since the function stored in callback will return number * 2,
	//the value being pushed into the results is going to be 8
	results.push( callback(singleValue) ); 
}
```

The fifth pass: 

```js
for(var i = 0; i < array.length; i = i + 1) {
	//i = 4;
	var singleValue = array[i]; //5
	//callback(singleValue) will be passing 5 as the value in singleValue
	//and since the function stored in callback will return number * 2,
	//the value being pushed into the results is going to be 10
	results.push( callback(singleValue) ); 
}
```

Once the `for` loop is done, it will have created an array of results that looks like this `[2,4,6,8,10]`.


