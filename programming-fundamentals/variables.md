<!-- Student takeaway: -->
<!--Student will be able to:
- Explain what a variable is
- Know at least 2 of the 3 variable declaration keywords
- Explain the difference between let and const
- Understand the difference between declaring a variable and assigning it a value
- Know the assignment operator 
- Know the arithmetic operators
- How to concatenate strings with + and with template literals
- That you can use a variable as a value in another variable
-->

# JavaScript variables

_Variables_ are like containers used to name and store data. The data can be accessed by referring to the name of the variable. 

If you write the words `myLunch` on your lunchbag, anything that goes in there is your lunch. The value of the variable `myLunch` will be different on any given day (i.e. it varies). You can be asked the exact same question every day (e.g. "What's in the bag labelled `myLunch`?") and your answer will change: `a ham sandwich`, or `leftover roti`, or `sushi, baby! `.

## Creating a variable
Before you're able to use a variable, you must be _declare_ it, then _assign_ it a value. Usually, you'll declare all your variables before you use them at the top of your JavaScript file.

### Declaring a variable
There are three [_keywords_](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Reserved_Words) (special words that are reserved by JavaScript to denote specific behaviours) we can use to declare a variable: `let`, `const`, and `var`. 

You choose the name of the variable. It should be something descriptive based on what kind of value it will hold:

```js
let email;
```

Type the above into your console. What does it return? `undefined`! 

> Remember,`undefined` is a **data type** that means it doesn't have a value. 

The console (a REPL environment) wants to evaluate everything we type in there and produce a value. When we define a variable in the console, we will always see `undefined` as the output at first, because we have only declared the variable.

_Reference_ the value of the variable we just created by typing `email`. What do you see? Nothing! 

### Assigning a value to a variable
To assign a value to a variable, we use the `=` operator:

```js
let anotherEmail;
anotherEmail = "hello@email.com";
```
*The value on the right hand side is stored in the variable on the left hand side.*

Once you have declared a variable with `let` you don't need to keep using that keyword when you're referencing that variable.

Now type `anotherEmail` into your console again:
```js
anotherEmail
```

We have assigned a value to `anotherEmail` which we can access by using that value's name.

```js
anotherEmail
// "hello@email.com"
```

Variables can also be declared and assigned a value in a single line of code:
```js
let threemail = "hiAgain@email.com";
// undefined
```

Why did the above example return undefined?   
Because `let threemail = "hiAgain@email.com";` is not an expression, it's a _statement_. The REPL evaluated it and came up with `undefined`. 

Like expressions, statements give instructions to the computer but statements don't always return a value (while expressions always do).

> Remember that an **expression** would be something like `5+7`. Type this in your console and you will see that it returns a value of `12`. 

We've already seen that *referencing* a variable name returns its value. What happens when you _assign_ a variable to a second value without using one of the declaration keywords? 

In other words, what do you think `yetAnotherEmail` will return here:
```js
let yetAnotherEmail = "hello@email.com";
yetAnotherEmail = 'hi@email.com';
yetAnotherEmail;
```
> Yep! It returns the second value, because `=` (re)assigns the value of the variable.

Notice that we've used both double and single quotes here. It doesn't matter which we choose, but we should stay consistent within our program:
```js
let yetAnotherEmail = "hello@email.com";
yetAnotherEmail = "hi@email.com";
yetAnotherEmail;
```
#### `const`

Along with `let` we can use `const` to declare variables. `const` will created a variable that is _read only_, meaning that you cannot change the value of it once it has been defined.

```js
const electronicMail = "sally@test.com";
electronicMail = "bryan@test.com";
```

This will throw an error `TypeError: invalid assignment to const 'electronicMail'`. 

For the most part in our JavaScript, we will be able to declare all our variables with `const`. When a case arises that forces us to use `let` we will *let* you know why! The reason we can use `const` for most every declaration is that we will not be reassigning values very often. So we can make our variables "safer" by creating constant version of them, reducing the possibility of them being overwritten.

#### `var`
`var` is a less-specific way of declaring variables and can be unpredictable in your programs. It's being phased out in favor of `let` and `const`; while sometimes you may see it in older code examples, we are only telling you about it so you know it exists. Don't use it!

### Variable naming conventions
* Variables can't contain spaces. They must start with a non-numeric character (letter, `_`, or `$)`, followed by any character. (e.g. `let 23people` is invalid).
* Use camelCase to separate words (e.g. `let myName`). Using underscores to_separate_words is a common convention in other programming languages (like PHP) but is generally avoided in JavaScript.
* JavaScript is case sensitive so variable names are also case sensitive.
* When naming a variable, it's best to give it a descriptive name. (e.g. `let userName` instead of `let u`).

Consider the following code: 

```js
const 8 = x;

```

The REPL will return an error when the syntax rules are not followed.

```js
SyntaxError: missing variable name
```
What? We gave it a name! But `8` is an invalid name so JavaScript just walks on by. 

## Using variables as values
After a variable is declared, it can be used as an expression in another variable. In the example below, `years` is being reused in the `days` variable.

```js
const years = 25;
const days = years * 365;
```

## Operators

You can do basic arithmetic with numbers using _operators_. Arithmetic operators in JavaScript are (`+`) for addition, (`-`) for subtraction, (`*`) for multiplication and (`/`) for division.

```js
55 * 20 

23.5 - 11

6 / 1.5

34 + 66.3
```

Parentheses can be used to group operations. Just like you learned in grade school, BEDMAS applies. This is the order in which the computer will do the math:

**B**rackets   
**E**xponents  
**D**ivision  
**M**ultiplication  
**A**ddition  
**S**ubtraction 

```js
(2+1) * 5
```

This is how you use exponents in Javascript:
```js
2 ** 5
```

> A fun gotcha! When numbers are contained within quotes, they are considered **strings**, meaning they can't be used to perform arithmetic operations.

```js
'2' + 2
'22'
```

What happens is JavaScript will convert the number `2` to be a string.


<!-- **Exercise**  
In pairs, solve the following questions by using operators. You can type all your equations into the console. 

> When in the console, press the up arrow on your keyboard to bring back the last run line of code.

- how many hours are in a year? 
- how many minutes are in a decade? 
- how many seconds old are you? 
 -->

## Concatenation
Unlike the other arithmetic operators, the `+` operator has two uses! In addition to... addition... it can also join strings, what's known as _concatenation_. If you use the `+` operator with only numerical values, it will add the values. Otherwise, it will combine the outputs as a string.

You can concatenate variables, strings, or a combination of both.

To join the three strings `"JavaScript"`, `"is"` and `"awesome!"` to get `"JavaScript is awesome!"` we would type:

```js
"Javascript " + "is" + " awesome!"
```

To join strings and variables, it would be:

```js
const language = "JavaScript";
const sentence = language + " is awesome!";
sentence;
```
	
What happens when you type the below expressions in the console?

```js
'HackerYou' * 6 
```

```js	  
'HackerYou' + 6
``` 

```js
'HackerYou' * 'Class'
```

`NaN` (not a number) for first and third examples. We can't do some operations (like multiplication) with types that are not numbers.

**Exercises**  
What happens when you type in the console: `'She's a HackerYou student'`. 

Error! How would you solve this issue?

### Template literals

In ES6 there is a new way to define a string, and it comes with some added benefits. Currently if you want to define a string, you can use `''` or `""`.

```js
const name = "Shauna";
const job = "bus driver";
```

If you want to concatenate strings together you can use the `+` operator. 

```js
const name = "Shauna";
const job = "bus driver";
const sentence = name + " works for the city as a " + job;
console.log(sentence);// "Shauna works for the city as a bus driver."
```

To create a template literal string, we use the backtick `` ` `` in place of the quotes. 

```js
const nameTwo = `Rukmini`;
const jobTwo = `streetcar driver`;
```

Strings and template literals behave in exactly the same way, but backticks make concatenation a lot easier. 

```js
const nameTwo = `Rukmini`;
const jobTwo = `streetcar driver`;
const sentenceTwo = `${name} works for the city as a ${job}`;
console.log(sentenceTwo);// "Rukmini works for the city as a streetcar driver."
```

Notice the `${}` syntax inside of the string - this is a _template expression_. It allows us to create a template for our strings. The browser will evaluate the `${}` expression and leave the proper value in its place at runtime. This makes concatenating large strings a lot more enjoyable.

### Whitespace
_Whitespace_ refers to blank characters and includes spaces, tabs, and line breaks. JavaScript usually ignores whitespace except when a *string* is being outputted into the browser.

Note how a spaces were added to the strings in the concatenation examples above.

**Exercise**: In the statement `let youveGotEmail = "meg@aol.com";`, which white spaces are optional and which are not?

## Bonus: multiline template literal strings

A fun extra thing is how template literals handle multiline strings. If you wanted a regular string to span more than one line, you would have to do something like this:

```js
const multi = "This is a \n multiline string";
console.log(multi);
```
You'd have to include the `\n` new line character. If you tried to put that on two lines:

```js
const multiForReal = "This is a \n 
multiline string";
console.log(multiForReal);
```

It would throw a very descriptive error `SyntaxError: "" string literal contains an unescaped line break`. 

However, template literals can use line breaks without escaping them:

```js
const tempLitMulti = `This is a 
multiline string`;
console.log(tempLitMulti);
```
😎😎😎😎😎😎😎😎😎

To learn more check out this [video](https://youtu.be/LTbnmiXWs2k?list=PL57atfCFqj2h5fpdZD-doGEIs0NZxeJTX) on `let` and `const` and template literals.

<!-- 
It's best practice to declare variables at the top of your code to avoid confusion. 
 -->


<!-- ## Some common errors
Have a look at the code below and see if you can spot the error. Then run the code and verify that you spotted an error. Fix the code and verify that it runs properly.

```js
const myName = "Homer";
myNme;
``` -->
