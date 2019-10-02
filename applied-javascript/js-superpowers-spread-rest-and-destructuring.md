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
const myArray = [68, 43, 5, 11];
const aTotallyNewArray = [...myArray];

myArray.push("a string");

console.log(myArray);
// [68, 43, 5, 11, "a string"]
console.log(aTotallyNewArray);
// [68, 43, 5, 11]
```






<!-- The difference between the spread operator and rest parameters is the difference between parameters and arguments. You use one to talk about the placeholders in a function (parameters/rest parameters) and you use one to talk about the actual values passed to a function (arguments/spread operator). -->