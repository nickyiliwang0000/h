# Callback functions

In programming, a *callback function* is a function that is passed as an argument to another function. A *callback function* is created in order to be executed at a later point in time. In JavaScript, this is often used for events.

An example of this might be a click event with jQuery.

```js
$('button').on('click', function() {
	// Do some work in here
});
```

Here we set up an event using the `on` method. The `on` method takes two arguments here, the first is a string describing the name of the event. In our case, the event is `click`. The second argument is what function we want to run when the click happens. *This function* is the callback function. 

When we provide the callback function to the `on` method, it has not run yet. The function is placed there as a value and only when we click the `button` will that function be called. 

Callback functions in JavaScript are functions that we are **passing as values** to other function or method calls.

So we could handle that above differently if we wanted.

```js
const handleClick = function() {
	// Do some stuff
}

$('button').on('click', handleClick);
```

First define the function `handleClick` and then *reference* this new function as the second argument of the `on` method. Notice that we do NOT use the `()`. Instead of calling the function, we are passing the value of `handleClick` inside of the `on` method, which happens to be a function. This function will be called when the click happens. 

## Making our own.

In order to further understand how callback functions work, let's write our own function that accepts a callback. 

Here we have a function that accepts one parameter. When we call it, we pass a string as an argument. 

```js
const doChores = function(chore){
	console.log(`I finished ${chore}.`);
}

doChores('sweeping floor');
// outputs "I finished sweeping the floor."

```

Now we have added another parameter, that is a function. 

```js
const doChores = function(chore, reward){
	console.log(`I finished ${chore}.`);
	reward();
}

doChores('sweeping floor', getDollars);
```

But we have not defined the `getDollars` function yet. Let's do that.


```js
const doChores = function(chore, reward){
	console.log(`I finished ${chore}.`);
	reward();
}

const getDollars = function(){
	console.log(`You earned $1.`);
}

doChores('sweeping floor', getDollars);
// outputs 
// "I finished sweeping the floor."
// "You earned $1."
```

In this case `getDollars` is a callback function.

Callback functions are especially useful if the executing function is taking place over a period of time, like waiting for a click to occur, for a set interval to finish or for API results to return.


## Advanced Examples

For a more advanced example, check out [how to rewrite the javascript array method, `.map()`](https://github.com/HackerYou/bootcamp-notes/blob/master/applied-javascript/rewriting-map-with-callbacks.md) using callback functions.

