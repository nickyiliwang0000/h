## Control Flow

Normally, instructions or **statements** in a JavaScript are executed one after the other, in the order in which they are written. 

**Control flow** is referring to the order of instructions that are executed based on a decision and is used to change the flow of statements. 

An example of a control flow statement is an if/else statement.

"If this condition is true, do this. Else, do this."

#### Booleans

Our code so far is executed top to bottom. If that's all we could do then our programs would be limited. This is where **control flow** comes in. We can write code so that a statement or group of statements is only executed if a logical condition is true or false.

A type of value that we need for conditionals is the **boolean** type. This type has two possible values: `true` or `false`. For example, when checking if two numbers are equal the value returned should be either true or false. How to we check it two numbers are equal? We use comparison operators.

#### Comparison operators

Operator     |  Description  
------------ | -------------
==	 | is equal to 
===	 | is exactly equal to (value and type)
!=	| is not equal to
!==	| is strictly not equal to
\>	| greater than 
<	| less than
\>=	| greater than or equal to	
<=	| less than or equal to



Check equality with `===` (equal) and `!==` (not-equal). Note how we **do not use regular equals**. Why?

Check inequality with `>=` `<=` `>` `<` (greater than and less than)

**Exercises**: In the console, write two expressions that return the boolean value `false` and two that return `true`.

#### Combining boolean expressions

In order to make more complex conditions we can use logical operators to check for something like. If `2 is equal to 2 AND 3 is greater than 1`.

**Logical operators**  

&&  = **AND** <br>
|| =  **OR** <br>
!   = **NOT** <br>

We can combine boolean expressions using (`&&`) and (`||`) operators.

Most often you will use `&&` to determine if two statements are both true, for example:

```js
const cow = "mammal";
const feet = 4;

cow === "mammal" && feet > 2 // returns true, since cows are mammals and they have more than two feet

cow === "mammal" && feet > 6 // returns false, because even though cows are mammals, they have fewer than 6 feet!
```

Most often you will use `||` in situations where you only care if at least one of the conditions is true, for example:

```js
const age = 30;
const name = "Steve";

age > 25 || name === “McLovin”
```

This will return true if EITHER the age variable is greater than 25 AND/OR the name variable is equal to “McLovin”.

The only time an `||` will return false is if NEITHER condition is true. So if age is less than 25, AND name is not equal to “McLovin”, this statement will return false.

**NOTE:** One fun and weird quirk of JavaScript is that every value in JavaScript can be compared to any other value in JavaScript. For example, `0`, `null` and `undefined` will all evaluate to ‘false', whereas any string (`“Kristen”`, `“pizza”`), or any number higher than `0` will evaluate to true.

Values that evaluate to false (like `0`, `null`, and `undefined`) are known as `falsey` values, whereas values that evaluate to true (any number bigger than 0, strings, etc.) are considered `truthy` values.

This might seem strange at first, but we'll learn more about why this is useful in the coming lessons.

### Conditional statements
Now that you're familiar with booleans, it's time to meet **conditional statements**. Simply put, these statements allow us to run a statement or group of statements only when a condition is true or false.

Here is the syntax for an if/else statement:

```js
if (condition) {
  // block statement (do something)
} else {
  // block statement (do something)
}
```


Let's break that down.

1. `if` is a keyword
2. `condition` is usually a boolean expression
3. `block statement` will be explained below
4. `else` is a keyword. 
5. another `block statement`. Note that the `else` block is optional.


![image](https://hychalknotes.s3.amazonaws.com/control-flow.png)

#### Block Statements
A block statement is used to group statements (instructions). The block is delimited by a pair of curly brackets `{}`:

```js
if ( time === 'morning') {
  // do all of the following things
  console.log("Good morning!");
} else {
  // do all the following things if the first condition is false
  console.log("Good evening!");
}
```

In fact a block statement could be just the `{}`.

```js
{
  console.log('Hi!');
}
```

**Exercises**: Complete the following exercises in pairs. Put your code between `<script>` tags inside of an HTML file.


1. Consider the code below; what is printed to the console?

```js
const n = 4;

if (n > 10) {
  console.log("That's a big number");
} else {
  console.log("It's a small number");
}
```


2. Create a quizzing program. The program asks a question, the user is prompted to answer, the answer is checked and then a score is printed to the console.

3. Consider the code below; what is printed to the console? What is `else if`?

```js
const n = 55;

if (n > 100) {
  console.log("That's a big number");
} else if (n > 10 ) {
  console.log("It's kinda big");
} else {
  console.log("It's a small number");
}
```

4. Create a simple "rock-paper-scissors" game. Prompt the user to enter their choice of "rock", "paper" or "scissors" and store this value in a variable. Always compare the user's input with the value "rock" (we'll work on making this more dynamic later). If the user's input is "paper" then print to the console "You Win!". If the input is "rock" then print "Tie" and print "You Lose" if the user's input is "scissors". 

## Loops

Another powerful concept in programming is **loops**. With loops, a block of statements are repeatedly executed while a condition is true.

![Loops](https://hychalknotes.s3.amazonaws.com/loops.png)


## For Statements

```js
for (initialExpression; condition; incrementExpression) {
  // loop statements
}
```

When a **for loop** executes, the following happens:

1. The **initialExpression** is typically used to initialize (start) a counter variable. *This expression can also declare variables with the `let` keyword.* 

2. The **condition** is an expression that is evaluated before each loop iteration. If this expression evaluates to true, the statement is executed. If this expression evaluates to false, the `for loop` ends.

3. The **incrementExpression** is evaluated at the end of each loop iteration. Generally used to update or increment the counter variable.

Let's look at an example:

Before running the code below predict what would happen. 

```js
for (let i = 0; i < 10; i = i + 1) {
  console.log(i);
}
```

When would you want to use this? Let's say you have a music playlist containing 10 songs. You want the playlist to queue up the songs. The `for` loop may look something like this:

```js
for (let i = 0; i < 10; i = i + 1) {
  queueNextSong(i);
}
```

`let i = 0;` Start at the first song.   
`i < 10` If the song that is queued is less than 10, you are not at the end of the list yet, so queue up the next song.    
`i = i + 1` To move to the next song on the list, add 1 to the current index number to move onto the next song.

**Exercises**:
Complete the following exercises in pairs.

**Level 1** Log into the console the numbers between 5 and 12.

**Level 2**. Log into the console the numbers between 1 and 10 in reverse (i.e. starting with 10). The output should look something like this:

```js
10
9
8
7
6
5
4
3
2
1
```

**Level 3**. Print the even numbers between 1 and 20. The output should look something like this:

```js
2
4
6
8
10
12
14
16
18
20
```

_Hint: Look up the modulo operator and use an if statement._

**Level 4**. Print the numbers from 1 to 100. But for multiples of 3 print “Fizz” instead of the number and for the multiples of five print “Buzz”. For numbers which are multiple of both 3 and 5, print “FizzBuzz”. The output should look something like this:

```js
1
2
Fizz
4
Buzz
Fizz
7
8
Fizz
Buzz
11
Fizz
13
14
FizzBuzz
...
```

_Hints: Look up combining boolean expressions with &&. Also look up modulo._


## While Statements

```js
while (condition) {
  // loop statements
}
```

A while loop is much simpler. The block executes repeatedly as long as the condition is true.

**DANGER!!** If the condition is never false then the while loop will keep going and your browser will crash. This is called an **infinite loop**. If you do get an infinite loop then go to "Window => Task Manager" in the browser, select the Task that is using a lot of CPU and click "End Process".

Let's look at an example:

```js
let i = 0;
while (i < 10) {
  console.log(i);
  i = i + 1;
}
```

When `i === 9` the block executes one final time, 9 is printed and `i` is incremented to 10. The block doesn't execute anymore because the condition is false BUT the value from the last executed expression is returned (that's why `10` has a little arrow beside it).

## Break Statements

We can terminate a loop at any time by using the break statement. For example:

```js
let number = 23;
while (true) {
  number = number + 1
  if (number % 9 === 0) {
    break;
  }
}
```

The above example would be an infinite loop (because true is always true!) but the break statement terminates the loop when the number is divisible by 9. The returned value (27) is greater than 23 and divisible by 9.

