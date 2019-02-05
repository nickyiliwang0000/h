<!-- Student takeaway: -->
<!--Student will be able to:
- Name the three standard color formats
- Identify which of the three standard color formats accept alpha values
- Use a alpha channel color to make a heading's background partially see-through
 -->
# Arrays and methods

## Arrays

Imagine that you wanted to make a list of values where the **order mattered**. You could use and object and do this:

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

So what are the differences between a regular object and an array object?

1. There are no property names (i.e. keys), so each spot in the array has a unique _index_ number that identifies it. JavaScript (and many other programming languages) are zero-based, which means that the first items in the array has an index of 0, not 1. 
1. Because variable names can't have numbers in them, dot notation doesn't work with arrays. `musicObject[0]` will get us the first item in the array. `musicObject.0` will not.

### Exercise

Download and complete the exercises [here](https://hychalknotes.s3.amazonaws.com/beginner-array-exercises.zip).

## Methods

### Functions review

Let's take a small detour and talk about functions. Functions in JavaScript are objects. This means that like a number, string, or array, they can be stored in variables.

`function myFunction(){}` creates a function and makes it available anywhere in our code. This way of defining a function is called a function declaration.  We can also use function expressions to define functions. 

`const myFunction = function(){}`. This means take this function object and put it in the "myFunction" box so that we can get at it whenever we want. 

#### Reference function
If we write `myFunction` then we get back an object. Define a function using a function expression in your chrome console and  then type its name without the parenthesis. Do you see that you get the function back?

#### Call function
`myFunction()` calls the function and we get back the result of the function. The only difference is the added parenthesis `()`.

#### Method

We already know that objects can hold strings, numbers and arrays. Now we will learn that objects can also hold functions. 

A function that is a property of an object is called a **method**. 

Once more: Any time a function is in an object, we call it a method. It does the same thing, just called something different. So, for ease of understanding right now a method is a function.

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

Notice that the method is **not** defined with a name. This is called an **anonymous function**. It's simply referred to by the key in the object. 

Here is an object for a Rageddy Ann doll where we use a function to convert height from centimetres to inches. 

```js
const raggedyAnn = {
  hairColor : "red",
  age : 8,
  height : 24,
  getHeightInInches : function() {
    return raggedyAnn.height * 0.393701; // converts CM to Inches
  }
}
```

#### Call methods

Calling a method is just as easy as saying the method name plus `()`.

We have already seen this with the object `console` and the method `log`:

```js
console.log();
```

What other methods are on console? Let's open dev tools to see.

With reference to the above ryan object:

```js
ryan.getHeightInInches();
```
### Built-in array methods
Most objects have built-in methods that do interesting work. We said earlier that an Array is an object. Arrays have some special built in methods.

#### Adding items to array with the `.push()` method.

To add an item to an array, we use push

```js
const myArray = [1, 3, 4];
myArray.push(5) //add value to the end;
myArray; //[1, 3, 4, 5];
myArray.unshift(0) //add value to the beginning;
myArray; //[0, 1, 3, 4, 5]
```

##### Do it again!

1. First, Create an empty array:

```js
const names = [];
```

2. Next, add the following names to it: Zoe, Ryan

```js
names.push("Zoe");
names.push("Ryan");
```

3. How would we get "Ryan"?

```js
names[1]; // why 1? Isn't it the 2nd item in the array?
```

4. We forgot to add Kristen. As an apology, we will add her to the front of the list. To do this, we can use unshift to **add to the front of an array**.

```js	
names.unshift("Kristen");
```

5. Now how would we access "Ryan"?

```js
names[2] //Why 2 now? And not 1 like before?
```


#### Removing items from array with `.pop()` and `.shift()`

We can push items on to the end of the array with `.push()`, and we can pop items off the end of the array with `.pop()`. If we want to get an item off the front of the array we need to use `.shift()`.

```js
const myArray = [1, "hi", 4, true];
myArray.pop(); //remove last value & return it;
myArray; //[1, "hi", 4];
myArray.shift(); //remove first value & return it;
myArray; //["hi", 4]
```

##### Do it again!

1. Let's start with	a base array of names:

```js
const names = ["Zoe","Ryan","Kristen","Adam","Tiff", "Danny", "Brandon"];
```

2. Let's get rid of "Zoe". Since she is the first item in the array:

```js
names.shift();
```

3. Is it gone? Type `names` into console again. See that "Zoe" is no longer there

4. What about getting rid of the last item in the array? Get rid of "Brandon". 

```js
names.pop();
```

#### More Array Methods

Arrays have a few more of methods to help you with managing your data, there are even more that we will discuss later.


| Method | Description |
|:-----------|:------------|
|concat() | 	Joins two or more arrays, and returns a copy of the joined arrays |
|indexOf() | 	Search the array for an element and returns its position |
|join() | 	Joins all elements of an array into a string |
|lastIndexOf() | 	Search the array for an element, starting at the end, and returns its position |
|pop() | 	Removes the last element of an array, and returns that element |
|push() | 	Adds new elements to the end of an array, and returns the new length |
|reverse() | 	Reverses the order of the elements in an array |
|shift() | 	Removes the first element of an array, and returns that element |
|slice() | 	Selects a part of an array, and returns the new array |
|sort() | 	Sorts the elements of an array |
|splice() | 	Adds/Removes elements from an array |
|toString() | 	Converts an array to a string, and returns the result |
|unshift() | 	Adds new elements to the beginning of an array, and returns the new length |
|valueOf() | 	Returns the primitive value of an array |

Bookmark the cheatsheet below: 

<a href="https://gist.github.com/ourmaninamsterdam/1be9a5590c9cf4a0ab42#file-arrayzing-md" target="_blank">https://gist.github.com/ourmaninamsterdam/1be9a5590c9cf4a0ab42#file-arrayzing-md</a>

<a href="https://devhints.io/js-array" target="_blank">https://devhints.io/js-array</a>

#### Array Exercise

Open [tv-show-arrays.html](https://hychalknotes.s3.amazonaws.com/tv-show-arrays-exercise.zip). Have fun manipulating the array using the above methods. The instructions are commented within the source code.

You will need to use `console.log()` to log it to the console as well as create your own variables when required. 

<!-- Your final output should look like this: -->

<!-- ![](http://wes.io/U1sB/content) -->

Let's start the first few together.

## Looping through an array

Arrays are useful for storing information and often we want to extract the data from them quickly.

```js
const myArray = ["item1", "item2", "item3"];
```

In the array above, if we wanted to get all the data out, we would have to write `myArray[0]`, then `myArray[1]`, then `myArray[2]`. This is not very effective.

Instead, we can use a `for` loop to iterate through the array items and extract the data within. 

```js
for (let i = 0; i < 10; i++) {
  
}
```

In the case of the array, we want to perform a task for every item inside and then stop. Within the loop conditional, we can use the array property, `.length` to provide us the number to stop at.

The `.length` property of an array is updated any time an element is added or removed from the array. Notice that it is not a method, it is just a property on the array.

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

## The 'this' Keyword

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

The `this` keyword is something that can be a little confusing, as the context, or value stored in `this` can change based on when you use it. 

When used inside of a method on an object the `this` keyword will refer to the object. However, when used inside of a function not on an object, `this` refers to something different. Try it and see what happens.

We will discuss `this` a little further in another lesson.

**Exercise**:

Create an object that represents a "warrior". This warrior has the following properties:

- equipment, an array containing the values "sword" and "shield".
- energy, defaults to the number 100
- location, an object with two properties: x and y. The values of x and y are numeric.
- a method `walk()` which updates the warrior's location. If the warrior's location is x:10 and y:5 then walk(2, 0) will update the location to x:12 and y:5.
- a method `strike()` which uses up energy. If the warrior's energy is at 100 then `strike(25)` will reduce the energy to 75.
- a method `pickUpEquipment()` which adds the argument (a string) to the equipment array.

### Want more practice? 

Try creating a **"student" object**. The student should have the following properties:
- **equipment** (array).
- **energy** (number).
- **grades** (number).
- **uniform** (object with top, bottoms, shoes properties).
- create a method that takes in **food (number of calories)** and then updates energy.
- create a method that takes in new **equipment** that will update our equipment array.
- create a method that will change the **uniform** (since everyday you wear something different).
- create a method study time that takes **time studied (minutes)** that will update our grades and deplete our energy. 
  - For every hour that you study, your grades go up by 5% (example: if your grade is 60, and you study an hour, your grade will be 63) .
  - For every hour you study, your energy goes down by 2.
  - **Bonus:** if your energy goes below 0, your grades go down (10%).
- what happens if you use the update uniform method to change something that doesn't exist in the uniform object?

<a href="https://hychalknotes.s3.amazonaws.com/studentANSWER.html.zip" download>We are linking the answer key here, but promise you will make your best attempt before checking it out!</a>
