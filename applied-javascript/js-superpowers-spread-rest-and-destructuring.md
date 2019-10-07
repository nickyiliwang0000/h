<!-- Student takeaway: -->
<!-- At the end of this lesson, the student will be able to:
- Understand rest parameters
- Understand spread
- Pluck a value from an object with destructuring
- Pluck a value from an array with destructuring
 -->

# JavaScript Superpowers: Spread, Rest and Destructuring

As we build increasingly complex JavaScript apps, we will run into situations where we deal with data sets of unpredictable size, or which require particularly lengthy code just to access the data. A few years ago, ES6 introduced some great tools we can use to cut down our workload and clean up our code.


## Spread operator

The _spread operator_ allows us to pass an array of arguments into a function as if we were doing it manually one-by-one. This is great because it saves time, plus it doesn't need to be rewritten every time the array changes.

Imagine you wanted to find the highest of the numbers in an array using `Math.max`:

```js
const numbers = [39, 25, 90, 123];
const max = Math.max(numbers);
console.log(max); // NaN
```

You can't! `Math.max` is a method which accepts a comma separated list of values, then returns the highest one. It doesn't know what to do when we pass it an array.

We could solve this by manually getting data out of our array:

```js
const numbers = [39, 25, 90, 123];
const max = Math.max(numbers[0], numbers[1], numbers[2], numbers[3]);
console.log(max); // 123
```

This is tedious, and if the array changes length, then we also need to update the argument list we're passing to `Math.max`.

Instead, we can use the spread operator. It is denoted by `...`, and it separates (spreads!) the items out of the array, so we can treat them as a list of individual values:

```js
const numbers = [39, 25, 90, 123];
const max = Math.max(...numbers);
console.log(max); // 123
```

The spread operator can pull apart all kinds of values:

```js
console.log(..."string");
// s t r i n g
```

```js
console.log(..."👩‍👩‍👧‍👧");
// 👩 ‍ 👩 ‍ 👧 ‍ 👧
```

One thing we'll often find ourselves using the spread operator for going forward is to make new copies of arrays. If we try to simply save an array to a new variable, we run into a problem:

```js
const myArray = [68, 43, 5, 11];
const copiedArray = myArray;

myArray.push("a string");

console.log(myArray);
// [68, 43, 5, 11, "a string"]
console.log(copiedArray);
// [68, 43, 5, 11, "a string"]
```

Changing our original array also changes our copy! This is because unlike primitive values, when we store arrays (as well as regular objects and functions) in variables, the variable still refers to the original object in memory. This is a problem because we probably made a copy of the array so that we could treat each one differently (for example, change one and save the other).

A simple solution to this is to spread our array out, creating a new set of individual values, and then to wrap those values in square brackets (collecting them into a new array):

```js
const yourArray = [68, 43, 5, 11];
const aTotallyNewArray = [...yourArray];

yourArray.push("a string");

console.log(yourArray);
// [68, 43, 5, 11, "a string"]
console.log(aTotallyNewArray);
// [68, 43, 5, 11]
```

`aTotallyNewArray` is exactly that - totally new. It is stored in a new space in memory, so it isn't affected when we alter the original array.


## Rest Parameters

_Rest parameters_ are like spread's cousin. They look similar (both use the `...` syntax), but where spread pulls the items out of an array passed as an argument, rest does the reverse - it lets us tell a function to gather the first, second, third and all the **rest** of our parameters, and store them in a array.

Imagine you want a function that takes any number of arguments and returns them in an array so that we can use `.map()`, `.filter()` and other powerful array methods on them:

```js
// I want this function:
arrayIt(3, 44, 81, 6, 19, 27);
// To result in an array like [3, 44, 81, 6, 19, 27] 
```

You'd probably end up writing a function that looks like this:

```js
const arrayItToMe = function(param1, param2, param3, param4, param5, param6) {
  const numbers = [param1, param2, param3, param4, param5, param6];
  console.log(numbers);
};

arrayItToMe(3, 44, 81, 6, 19, 27);
// [3, 44, 81, 6, 19, 27]
```

OK, this works, but what if somewhere else in our code we also want to call a function to return an array, but we only have 4 arguments to pass it? Or 10? We would have to write a whole new `arrayIt` function for each instance, which isn't clean or DRY.

Instead, we can make a single function that is more dynamic by using rest parameters. Adding the `...` before the name of a parameter, we can turn an array-like object of values (like a list of arguments) into an actual array!

```js
const arrayItRockapella = function(...numbers) {
  console.log(numbers);
};

arrayItRockapella(3, 44, 81, 6, 19, 27);
// [3, 44, 81, 6, 19, 27]

arrayItRockapella("any values work", true, {worth: 100}, "awesome, right?");
// ["any values work", true, {worth: 100}, "awesome, right?"]
```

The spread operator and rest parameters look the same, but the difference between them is the difference between parameters and arguments. You use one to talk about the placeholders in a function (parameters/rest parameters) and you use one to talk about the actual values passed to a function (arguments/spread operator).