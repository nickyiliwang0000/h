<!-- Student takeaway: -->
<!--Student will know:
- What control flow means
- What the comparison operators are (< > , =< =>)
- How == is different from ===
- What the logical operators are (&& || !)
- Syntax of a for loop
- Syntax of a while loop
- How to quit a browser that's got an infinite loop going on
- That a break statement exits a loop
-->

# Programming control flow

Normally, instructions (i.e. **statements**) in a JavaScript are executed one after the other in the order in which they are written. 

The term _control flow_ describes how a developer might choose to order the execution of statements, regardless of the order in which they appear in the JavaScript file.

An example of control flow is an `if` statement:
```js
if (time === 22) {
   goToSleep();
} else {
  learnMoreCode();
}
```
In this statment block, the `goToSleep` function is only executed if the variable `time` is 22 (i.e. ten o'clock at night), even though it appears in the script before `learnMoreCode`.

Let's dive into that logic!

## Conditional statements

The statement block above is a _conditional statement_, meaning that a  condition needs to be satisfied in order to run each function.

Here is the syntax for `if`/`else` statements:

```js
if (condition) {
  // block statement (do something)
} else {
  // block statement (do something)
}
```
![A diagram that describes the flow of an if/else statement](https://hychalknotes.s3.amazonaws.com/control-flow.png)

Some vocabulary:
* `if` and `else` are keywords
* `condition` will usually be an expression that evaluates to a boolean 
* `block statement` will be a chunk of code

The whole `else` block is **optional**! If you don't include an `else` block and the condition isn't met, the block statement after the `if` is ignored and the program moves on without doing anything further there.

### Block statements
A _block_ is used to group statements. The block is delimited by a pair of curly brackets `{}`:

```js
if ( time === 'morning') {
   // do all of the following things
   console.log("Good morning!");
   alert("It's morning!");
} else {
  // do all the following things if the first condition is false
  console.log("Hello!");
  alert("How are you!?");
  time = 'not morning';
}
```

In fact, a block statement could be just the `{}`.

```js
{
  console.log('Hi!');
}
```

### Comparison operators
The first step in using an `if`/`else` statement is defining the condition. A condition is usually a JavaScript expression that evaluates to a boolean (e.g. `true` or `false`). How do we evaluate the pieces of an expression? Using _comparison operators_.

Operator     |  Description  
------------ | -------------
`==` | is equal to 
`===` | is exactly equal to (value and type)
`!=`| is not equal to
`!==`| is not equal to (neither value nor type)
`>`| greater than 
`<`| less than
`>=`| greater than or equal to	
`<=`| less than or equal to

**Exercise**:
Compare two values using the `===` and `!==` operators. 

Compare two values using the `>=` and `<=` operators and then the `>` and `<` operators.

In the console, write two expressions that return the boolean value `false` and two that return `true`.

**Why can't we use `=` to compare values?**
> Because `=` is what we use to assign and reassign variables.

### Logical operators
We use logical operators to make more complex conditions for our statements.

<!-- Used bolding here and not `` because you have to escape the pipe character to be able to see it in the table. -->
Operator | Description
:---:|:---:
**&&** | and
**&#x7c; &#x7c;** | or
**!**  | not

We can combine boolean expressions using the `&&` and `||` operators.

Most often you will use `&&` to determine if two statements are **both** true, for example:

```js
const cow = "mammal";
const feet = 4;

cow === "mammal" && feet > 2 // returns true, since cows are mammals AND they have more than two feet

cow === "mammal" && feet > 6 // returns false, because even though cows are mammals, they have fewer than 6 feet!
```

Most often you will use `||` in situations where at least **one** of the conditions **must** be true:
```js
const age = 16;
const hasParentalPermission = true;

age > 18 || hasParentalPermission === true
// returns true
```

This will return true if **either** the `age` variable is greater than 18 **or** the `hasParentalPermission` variable is equal to `true`.

The only time an `||` will return false is if **neither** condition is true. So if `age` is less than 18, **and** `hasParentalPermission` is not equal to `true`, this statement will return `false`.

### Comparing values in JavaScript
Any value in JavaScript can be compared to any other value in JavaScript, even when the comparison doesn't make sense:
```js
//is this boolean larger than this string?
true > 'something'
//false

// is this number smaller than undefined?
0 < undefined
// false

// is this number roughly equal true?
1 == true
// true
```

Data type  | Value
---|---
`null` | `false`
`undefined` | `false`
any `string`| `true`
the `number` 0 | `false`
any `number` higher than 0 |`true`

Data types and values that evaluate to false (i.e. `0`,`null`, and `undefined`) are known as _falsy_, whereas data types and values that evaluate to true (i.e. strings, any number higher than 0) are known as _truthy_. This is why the `===` operator exists: it checks for equality in both type **and** value; `==` checks for equality **only** in value.

```js
let num = 0;
if ('string' && num === 0){
    console.log('the string evaluates to true')
  } else {
    console.log('the string evaluates to false')
  }
// returns "the string evaluates to true"
```
### Exercises
Complete [these](https://hychalknotes.s3.amazonaws.com/control-flow-exercises.zip) exercises in **pairs**. Practice pair programming! 

> Try having the person who feels **less confident** with JavaScript do the typing. It's the job of the person who feels more confident to gently guide the typer. 

## Loops
Another powerful concept in programming is _looping_. A loop runs a block of statements repeatedly while a condition is true.

![A diagram that describes the flow of a loop](https://hychalknotes.s3.amazonaws.com/loops.png)

### `for` loops
This is the syntax for a `for` loop:

```js
for (initialExpression; condition; incrementExpression) {
  // loop statements
}
```
Some vocabulary:
* The **intial expression** is typically used to initialize a counter variable.
  * This expression can also declare variables using the `let` keyword.
* As in an `if` statement, the **condition** is an expression that is evaluated to a boolean. 
  * The expression is evaluated before each loop iteration. 
  * If it evaluates to true, the statement is executed. 
  * If it evaluates to false, the `for` loop ends.
* The **increment expression** generally describes how the counter variable should change at the end of each loop. 
  * It usually adds `1` to the variable.

Predict what this `for` loop will produce:

```js
for (let i = 0; i < 10; i = i + 1) {
  console.log(i);
}
```

Let's say you have a music playlist containing 10 songs. You want the playlist to queue up the songs one by one. The `for` loop may look something like this:

```js
for (let i = 0; i < 10; i = i + 1) {
  queueNextSong(i);
}
```
* The intial expression `let i = 0;` means the loop starts with the index of the first song.   
* The condition `i < 10` is evaluated to see if it is true that the index of the song that is queued is less than 10. 
  * If true, there are more songs to queue up. 
  * If false, the loop will return.
* The increment expression `i = i + 1` tells the variable `i` to increase by 1 so the loop can be run for the next song.

### Exercises
Complete [these exercises](https://hychalknotes.s3.amazonaws.com/for-loop-exercises.zip) in pairs.

### `while` loops
A while looks is very similar to a `for` loop, but with even less information:
```js
while (condition) {
   // block statement
}
```
The block executes repeatedly as long as the condition is true.


<h3 align="center"> 
🚨🚨🚨🚨🚨🚨🚨🚨  DANGER 🚨🚨🚨🚨🚨🚨🚨🚨
</h3>

If the condition is never false, a `while` loop will run forever and your browser will crash. This is called an _infinite loop_. If you do get an infinite loop, quit your browser with `ctrl + Q` or `cmd + Q`. Sometimes Firefox will give you a little yellow tooltip that asks if you want to quit the process. You do!


![Screenshot of a tooltip in Firefox asking if you want to quit the browser](https://hychalknotes.s3.amazonaws.com/firefox-browser-crash-tooltip.png)


* If you can't quit from the browser on a Mac, go to 'Activity Monitor', select the browser in question, and force it to quit.
* On PC, `ctrl + shift + esc` will bring up the Task Manager. Choose your browser and click 'End Task'.

Let's look at an example of a non-infinite `while` loop:

```js
let i = 0;
while (i < 10) {
  console.log(i);
  i = i + 1;
}
```

When `i === 9` the block executes one final time, 9 is printed and `i` is incremented to 10. The block doesn't execute anymore because the condition is false.

Note that after printing `1` through `9` in your console, there's a `10` with a little arrow beside it. That's not a return, we can't directly capture that value. This is your dev tools console trying to be helpful by printing the last expression it executed.

## The `break` keyword

We can terminate a loop at any time by using a _break statement_:
```js
let number = 23;
while (true) {
  number = number + 1
  if (number % 9 === 0) {
    break;
  }
}
```
The above example **would** be an infinite loop (because `true` is always true!) **but** the break statement terminates the loop when the number is divisible by 9. 

The returned value (27) is greater than 23 and divisible by 9.

