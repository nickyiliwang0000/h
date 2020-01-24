## ES6

### The ECMAScript Standard

JavaScript was created in 10 days. Because of this there are a few issues with the language. Over the years there have been some additions to the language, but for a good long time there was nothing going on.

JavaScript is not actually called JavaScript, it's official name is ECMAScript (**E**uropean **C**omputer **M**anufacturers **A**ssociation). As a part of this organization there is a committee in charge driving JavaScript forward, they are called TC39 (Technical Committee 39. Badass name, right?!).

In June 2015, the TC39 committee finalized the sixth version of the ECMAScript spec, one of the biggest additions to date. It introduced quite a few new features to the language. These additions include new methods on Objects and Arrays, new function syntax, keywords like `let` and `const`, and much, much more. 

Most browsers have started to implement these features, but they can be slow to do this. Do not fear! Tools like [Babel](https://babeljs.io/) allow us to write modern ES6 code and will perform a task called *transpiling* which takes our code and rewrites it so that **any** browser can understand it. Kind of like how Sass works: you write this nice Sass syntax, but the compiler dumbs it down to plain ol' CSS for the browser.

## let and const

`let` and `const` are two new keywords that are available in ES6. There is one key feature these variables share that sets them part from `var`, a concept called block scope.

When you use the `var` keyword to create a variable it is function scoped. Meaning it will be available within the function it was created in and and function in that. But it is NOT available outside of there.

One common issue people will run into with function scoped variables is the `for` loop.

```js
for(var i = 0; i < 10; i++) {
	console.log(i);
}
console.log(i); // Will print out 10;
```

It is common to declare a variable inside of the for loop with the intent of it being just bound to that for loop. However that is not that case. If you run the above code you will see the `i` variable is available outside of the for loop.

#### Enter `let` and `const`

If you remember a block in JavaScript is anything between `{ }`. So when we talk about block scope, that means that any variables defined in these blocks will only exist in the block!

```js
{
	let name = "Ryan";
}
console.log(name); //Nothing appears
```

When you define a variable with the `let` keyword it will create a new variable only within the `{ }` or block. So going back to our `for` loop example.

```js
for(let i = 0; i < 10; i++) {
	console.log(i);
}
console.log(i); // Will print out ( Uncaught ReferenceError: i is not defined )
```

Other than that it will behave exactly like a variable defined with `var`.

The `const` keyword behaves the exact same way, with one exception. Once the value is defined, it can never be redefined. It is a read only value.

```js
const person = 'Ryan';
person = 'Kristen'; //Uncaught TypeError: Assignment to constant variable.
console.log(person);
```

The browser will throw an error if you try to reassign a value to a variable defined with `const`.

#### When to use `let` and when to use `const`

There is a bit of debate going on right now about when to use `let` vs `const`. The general rule of thumb is that if you know the value will not be redefined throughout your program, go with `const`, if you need a value that might change, go with `let`.


To learn more check out this <a href="https://youtu.be/LTbnmiXWs2k?list=PL57atfCFqj2h5fpdZD-doGEIs0NZxeJTX">video</a> on `let` and `const` and template literals.

## Template Literals

In ES6 there is a new way to define a string, and it comes with some added benefits. Currently if you want to define a string, you can use `''` or `""`. Basically just pick double or single quotes and stick with it.

```js
const name = "Ryan";
const job = "Instructor";
```

If you want to concatenate strings together you can use the `+` operator. 

```js
const name = "Ryan";
const job = "Instructor";
const sentence = name + " works at Juno as an " + job;
console.log(sentence);// "Ryan works at Juno as an Instructor"
```

To create a template literal string, we use the backtick `` ` `` in place of the quotes. 

```js
const name = `Ryan`;
const job = `Instructor`;
```

They behave exactly the same, but there is one difference. With a template literal, concatenation becomes a lot easier. 

```js
const name = `Ryan`;
const job = `Instructor`;
const sentence = `${name} works at Juno as an ${job}`;
console.log(sentence);// "Ryan works at Juno as an Instructor"
```

Notice the `${}` syntax inside of the string, this is a template expression. It allows us to template out our strings, and the browser will replace the `${}` expression with the proper value at runtime. This makes concatenating large strings a lot more enjoyable.

#### Multi line

One last thing to look at is how template literals handle multi line string. With a regular string if you wanted to have to span more than one line, you would have to do something like this.

```js
const multi = "This is a \n multiline string";
console.log(multi);
```
We have to include the `\n` new line character. If you tried to put that on two lines:

```js
const multi = "This is a \n 
multiline string";
console.log(multi);
```

It would throw an error `Uncaught SyntaxError: Unexpected token ILLEGAL`. However with template literals we CAN do that!!

```js
const multi = `This is a 
multiline string`;
console.log(multi);
```

So nice!!

To learn more check out this <a href="https://youtu.be/LTbnmiXWs2k?list=PL57atfCFqj2h5fpdZD-doGEIs0NZxeJTX">video</a> on `let` and `const` and template literals.

## Arrow Function

Arrow functions are a new syntax for creating functions in ES6! Now, this is not going to replace the `function() {}` we know and love! But we will be seeing them more and more and the defacto function syntax.

```js
const add = (a,b) => {
	return a + b;
};
```

The core part of the syntax is the lack of the `function` keyword when defining a new function. Instead, we have the `=>` or fat arrow. There are actually a few ways you can define the arrow function.

For example, if the function simply returns and there is nothing else in the function body, we can remove the `{}` around it and make it one line and remove the `return` keyword.

```js
const add = (a,b) => a + b;
```

If the function only had one parameter you can actually leave the `()` off it as well.

```js
const add5 = a => a + 5;
```

If there are no parameters however, you will have to include all the parenthesis.

```js
const eight = () => 3 + 5;
```

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
