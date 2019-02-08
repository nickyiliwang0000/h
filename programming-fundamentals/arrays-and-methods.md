<!-- Student takeaway: -->
<!--Student will be able to:
- Create an array
- Explain that a method is a function on an object
- Write a method
- Correctly use push pop shift and unshift
- Correctly write a for loop 
- Identify that .length is a property not a method
- Use .length correctly
- Use the keyword `this` with a method they wrote
 -->
# Arrays and methods

## Arrays

Imagine that you wanted to make a list of values where the **order mattered**. You could use and object an do this:

```js
const musicObject = {
  "0": "do",
  "1": "re",
  "2": "mi",
  "3": "fa",
  "4": "sol",
  "5": "la",
  "6": "ti",
  "7": "do"
}
```

Using an object we could enforce some order by setting the keys of the properties to be numbers. BUT, you may remember that there is **no guarantee** that an object will return properties the same order they were written when iterated over. Thankfully JavaScript has a built-in data type called an _array_ that maintains its order:

```js
const musicObject = [
  "do",
  "re",
  "mi",
  "fa",
  "sol",
  "la",
  "ti",
  "do"
]
```

Or, to save space:

```js
const musicObject = [ "do", "re", "mi", "fa", "sol", "la", "ti", "do" ]
```

> **An array is a kind of object** in JavaScript. Remember when we said objects are a big deal? They are! Everything in JavaScript is an object! Even arrays! Which are, like, the opposite of objects! 😱😱😱 Sorry!

As with regular objects, any kind of value (e.g. objects, numbers, string, other arrays...) can be stored inside of an array.

So, what are the differences between a regular object and an array object?

1. There are no property names (i.e. keys), so each spot in the array has a unique _index number_ that identifies it. JavaScript (and many other programming languages) are zero-based, which means that the first item in the array has an index of 0, not 1. 
1. Because variable names can't have numbers in them, dot notation doesn't work with arrays. `musicObject[0]` will get us the first item in the array. `musicObject.0` will not.

### Exercise

Download and complete the exercises [here](https://hychalknotes.s3.amazonaws.com/beginner-array-exercises.zip).

## Methods

### Functions review

Let's take moment to review [functions](https://github.com/HackerYou/bootcamp-notes/blob/master/programming-fundamentals/functions.md).

This is a **function declaration**:
```js
function myFunction(){
  //some code
}
```
It creates a function that can be referenced anywhere in our code using the function name `myFunction`.

This is a **function expression**:
```js
const myFunction = function(){
  //some code
}
```
It creates a function with no name and stores it in a variable named `myFunction`. 

<!-- I don't understand why this is here in the notes. This is the first time we talk about a function being an Object.  -->
<!-- #### How to reference a function
When we define a function in our browser console, and then press enter, `undefined` is returned, because declaring a function is a statement. When we type the function name or variable name and hit enter, what do we get back?

> An object!

Go ahead and try this. Click the triangle next to the function name to see that the function's prototype is `Object`.  -->

#### How to call a function
Adding smooth brackets to the function name like so: `myFunction()` is how we **call** the function. When we call a function, we get a return from it.

### What is a method?

We already know that objects can hold strings, numbers, and arrays. Now we will learn that objects can also hold functions!

There's a special name for a function that is a property of an object: a _method_.

We define methods like this:
```js
const myObject = {
  key1: value1,
  key2: value2,
  key3: function() {
    // do something
  }
}
```

Notice that the method is **not** defined with a name. This what's known as an _anonymous function_. It's referred to by the key in the object. 

Here is an object for a Rageddy Ann doll where we use a function to convert height from centimetres to inches. 

```js
const raggedyAnn = {
  hairColor : "red",
  age : 8,
  height : 24,
  getHeightInInches : function() {
    return raggedyAnn.height * 0.393701; // converts cm to inches
  }
}
```

### Familiar methods

Calling a method is the same as calling a function that is not stored in an object: add `()`.

We have already seen a few methods:

```js
console.log();
Math.random();
```

What other methods exist in the console object? Let's open dev tools to see.

With reference to the above `raggedyAnn` object:

```js
raggedyAnn.getHeightInInches();
```
> Note that you can't call a method without its object. Add that`raggedyAnn` object to your console and try running `getHeightInInches()` by itself.

## Arrays and methods
We said earlier that an array is a kind of JavaScript object; this is why arrays have some special built-in methods.

### Adding items: `.push()` and `.unshift()`

To add an item to an array, we use `.push()`

```js
const myArray = [1, 3, 4];
myArray.push(5) //add value to the end;
myArray; //[1, 3, 4, 5];
myArray.unshift(0) //add value to the beginning;
myArray; //[0, 1, 3, 4, 5]
```
**Exercise:**
1. First, create an empty array:

```js
const egyptianGods = [];
```

2. Next, add the following names of Egyptian gods to it: `Hathor` and `Bastet`.

```js
egyptianGods.push("Hathor");
egyptianGods.push("Bastet");
```
3. How would we get `Bastet`?

```js
egyptianGods[1]; // why 1? Isn't it the 2nd item in the array?
```

4. We forgot to add Taweret! As an apology, we will add her to the front of the list. To do this, we can use `unshift()` to **add to the beginning of an array**.

```js	
egyptianGods.unshift("Taweret");
```

5. Now how would we access `Bastet`?

```js
egyptianGods[2] //Why 2 now? And not 1 like before?
```

### Removing items: `.pop()` and `.shift()`

We can push items on to the end of the array with `.push()`, and we can pop items off the end of the array with `.pop()`. If we want to get an item off the front of the array we need to use `.shift()`.

```js
const myArray = [1, "hi", 4, true];
myArray.pop(); //remove last value & return it;
myArray; //[1, "hi", 4];
myArray.shift(); //remove first value & return it;
myArray; //["hi", 4]
```

**Exercise:**

1. Let's start with	a base array of names:

```js
const names = ["Zoe","Jenny","Brent","Adam","Asaf", "Fatima", "Charlotte"];
```

2. Let's get rid of "Zoe". Since she is the first item in the array:

```js
names.shift();
```

3. Is it gone? Type `names` into console again. See that "Zoe" is no longer there

4. What about getting rid of the last item in the array? Get rid of "Charlotte". 

```js
names.pop();
```

### More array methods

Arrays have lots more methods to help you with managing your data! Look up what kind of arguments each one can take [at MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/pop). The sidebar titled 'Methods' will have each one.

Here are a handful of common ones:

| Method | Description |
|:-----------|:------------|
|`concat()` | 	Joins two or more arrays, and returns a copy of the joined arrays |
|`indexOf()` | 	Search the array for an element and returns its position |
|`join()` | 	Joins all elements of an array into a string |
|`lastIndexOf()` | 	Search the array for an element, starting at the end, and returns its position |
|`pop()` | 	Removes the last element of an array, and returns that element |
|`push()` | 	Adds new elements to the end of an array, and returns the new length |
|`reverse()` | 	Reverses the order of the elements in an array |
|`shift()` | 	Removes the first element of an array, and returns that element |
|`slice()` | 	Selects a part of an array, and returns the new array |
|`sort()` | 	Sorts the elements of an array |
|`splice()` | 	Adds/Removes elements from an array |
|`toString()` | 	Converts an array to a string, and returns the result |
|`unshift()` | 	Adds new elements to the beginning of an array, and returns the new length |
|`valueOf()` | 	Returns the primitive value of an array |

Bookmark this array methods cheatsheet either one of these array methods cheat sheets.
* <https://devhints.io/js-array>
* <https://gist.github.com/ourmaninamsterdam/1be9a5590c9cf4a0ab42#file-arrayzing-md>

### Array methods exercise

Open [tv-show-arrays.html](https://hychalknotes.s3.amazonaws.com/tv-show-arrays-exercise.zip). Have fun manipulating the array using the above methods. The instructions are commented within the source code. (You may need to do a bit of Googling.)

You will need to use `console.log()` to log values to the console as well as create your own variables when required. 

<!-- Your final output should look like this: -->

<!-- ![](http://wes.io/U1sB/content) -->

Let's start the first few together.

## Looping through an array

Sometimes we want to target each item in an array one by one.

```js
const myArray = ["item1", "item2", "item3"];
```

If we wanted to print all the data out of `myArray`, we would have to:

```js
console.log(myArray[0]);
console.log(myArray[1]]);
console.log(myArray[2]);
```
This is not very efficient. We're repeating ourselves all over the place!

Instead, we can use a `for` loop to iterate through the array items and extract the data within. 

Remember that the syntax for a `for` loop is this:
```js
for(initialExpression; condition; incrementExpression){
// some code
}
```

In the case of the array, we want to perform a task for every item inside and then stop. Within the loop conditional, we can use the array property `.length` to provide us the number to stop at.

The `.length` property of an array is updated any time an element is added or removed from the array. Notice that it **is not a method**, it is a **property** on the array object.

```js
for (let i = 0; i < myArray.length; i++) {

}
```

Now inside the loop, we can use the variable that holds the iterated value. In the example, the `i` can be used to provide an index for us to reference a value in the array. Each iteration of the `for` loop will increase the value of `i`, this way we can access the properties of our array!

```js
for (let i = 0; i < myArray.length; i++) {
  console.log(myArray[i]);
}
```

## The `this` keyword

Inside of an object there is a special way to reference itself, the keyword `this` refers to that object. This can be used to update an object's properties. For example:

```js
const myBasket = {
  apples: 1,
  increment: function() {
    this.apples += 1
  }
}
```

```js
myBasket.apples; //1
myBasket.increment();
myBasket.apples; //2
```
The `this` keyword is a **variable**, so it can change in different contexts.

When used inside of a method on an object, the `this` keyword will refer to the object. However, when used inside of a function not on an object, `this` refers to something different. Try it and see what happens.

We will discuss `this` in more depth in our [scope and execution context lesson](https://github.com/HackerYou/bootcamp-notes/blob/master/applied-javascript/advanced-js-lexical-scope-and-execution-context.md).

### Exercise
Create an object that represents a "warrior". This warrior has the following properties:

- equipment, an array containing the values "sword" and "shield".
- energy, defaults to the number 100
- location, an object with two properties: x and y. The values of x and y are numeric.
- a method `walk()` which updates the warrior's location. If the warrior's location is x:10 and y:5 then walk(2, 0) will update the location to x:12 and y:5.
- a method `strike()` which uses up energy. If the warrior's energy is at 100 then `strike(25)` will reduce the energy to 75.
- a method `pickUpEquipment()` which adds the argument (a string) to the equipment array.


### Want more practice? 
[Download and complete this exercise](https://hychalknotes.s3.amazonaws.com/method-practice-exercise-bootcamp.zip) to practice creating an object with methods on it.

<!-- What happens if you use the update uniform method to change something that doesn't exist in the uniform object? -->
