<!-- Student takeaway: -->
<!--Student will be able to:
- What a programming language is (as opposed to a style sheet language or a markup language)
- That a REPL is a place to test out code
- That syntax is important
- What pseudo code is and to write it in the comments
- The data types we will be working with (SNUBON(S))
- The difference between an expression and a value
-->

# Intro to programming
*A programmer's partner sends them to the grocery store with instructions: "Get a litre of milk. If they have eggs, get a dozen."*

*The programmer comes home a short while later, an armful of milk cartons in tow.*

*"Why did you get so much milk?" the programmer's flabbergasted partner asks.*

*The programmer replies, "They had eggs."*

## A quick primer on programming languages

So far, we've created our projects using HTML (a markup language) and CSS, (a style sheet language) that have allowed us to add content to and style our web pages. If we want our web pages to do other things, things like responding to events, communicating with services, or modifying styles on the fly, we need to have a deeper conversation with the computer. 

We need a _programming language_. 

Programming languages are used to communicate a set of instructions to a computer. Computers' native language is a series of ones and zeroes. Programming languages allow us to bridge the gap between our native languages and computers' native language.

There are many different programming languages that are used for different kinds of projects: Objective-C and Swift are used for programming iPhone apps. Java is used for programming Android apps. Web developers can use Ruby, Python, PHP, and Node.js for the back ends of websites and web applications. 

The JavaScript programming language is what we will use to communicate instructions to the browser for our websites and web applications.

## Syntax is important
Programming is like having a conversation in a foreign language with a native speaker of that language, so sticking to the rules (e.g. the _syntax_) of the language you're speaking is important. Computers are sticklers for proper syntax! 

Syntax generally differs across programming languages, but there are some places it overlaps: sort of like how _croissant_ means the same thing in English and in French.

Let's look at a classic programming example in a few different languages: printing the string `hello, world` for the developer to see.

### C 
```c
main() {
    printf("hello, world");
}
```

### Java 
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("hello, world");
    }
}
```
### JavaScript
```js
console.log('hello, world');
```

Some languages are more human-readable than others!

## The programmer's job
The role of a programmer is to think of a solution to a real-world problem and break the solution down into simple mechanical instructions that the computer can understand. The computer executes the programmer's instructions **exactly** as written.

### Think like a computer

As with learning a new spoken language, the best way to learn programming is real-world practice with a native speaker. To do this effectively, it helps to **think like a computer**. Human spoken language has rhyme, tone, irony, humour, homophones, and onomatopoeia to convey meaning; most programming languages do not. So we have to be much more explicit in programming than in English; we have to break instructions into very small steps when speaking a computer's language.

Imagine that an alien of average human intelligence but with **very basic English vocabulary** has landed in the classroom. How would you give this alien instructions for getting to the washrooms? Tell them it's "just down the hall"? What if they don't know what "hall" means? We'll have to be more specific. What are all the little steps that are involved in getting to the washroom?

Take these instructions:

* Get to the door.
* Open the door.
* Walk through the door.
* Turn to the left.
* Walk down the hall.
* Open the washroom door.

Maybe we even have to specify which door. 
* Get to the **classroom** door.
* ...etc.

Maybe the alien doesn't know how to "get". 
* Walk 10 steps
* Turn to right 
* Walk 3 steps
* Open the classroom door
* ...etc.

Maybe the alien doesn't know what a door is. And whose "right" did we mean?
* Walk forward 10 steps 
* Turn to your right
* Walk 3 steps through the hole in the wall

It seems like we're explaining things in **too** much detail, but this strategy is very helpful in translating things like "I want to save the user's picture to their profile when they click the green button" into a bunch of lines of code that accomplish that.

#### Exercise: Computerthink

In small groups, write out detailed step-by-step instructions for how to make a cheese and spinach omelette. We'll compare your answers together to see just how specific you can get!

### Invent the world, maybe
There's a quote attributed to Carl Sagan that goes: 
<blockquote>In order to make an apple pie from scratch, you must first invent the universe.</blockquote> 

While it's not true that you have to invent the universe every time you make a new website, even simple-seeming programs can require many, many steps to complete.

## JavaScript
The first iteration of the language that we know as JavaScript was developed over 10 days in 1995. Its purpose was to allow developers to add functionality and interactivity to the browser, something that was not possible at the time. You'll hear lots of people complain about JavaScript's faults, but for something that was created in a bit over a week, it's pretty impressive!

JavaScript's working draft name was `Mocha` and its first name when it went live in the Netscape Navigator browser was `LiveScript`. Colloquially it's known as JavaScript, but it's official name is actually `ECMAScript`; it is overseen and maintained by the European Computer Manufacturers' Association. (This isn't suuuuper important, but when you see the initialism `ES6`, you'll know that it stands for ECMAScript, spec 6, which is JavaScript!)

### TL;DR
```js
JavaScript === ECMAScript
```

#### More about JavaScript
* [A re-introduction to JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript) (just the Introduction for now)
* [JavaScript Overview](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/JavaScript_Overview)

## REPL

_REPL_ stands for read, eval, print, loop. A _REPL enviroment_ is an interactive environment in which you can type instructions for the computer. The computer will read, evaluate/run, and print the results of those instructions. Then the computer then makes itself ready for the next instruction (i.e. loops).

A JavaScript REPL is available in the dev tools of your browser. Open the JavaScript REPL by navigating to the 'Console' tab.

Your console will look slightly different depending on your browser, but there should be an an arrow bracket `>` or two `>>` with an input beside it. The cursor should start blinking when you click into the input. Give the computer a simple instruction like `1 + 1`, press enter. The REPL will return a value!

```js
> 1 + 1
// 2
```

Cool, right?! This is a great environment you can use to test out your fledgling JavaScript skills.

## The DOM

DOM stands for **document object model**, and it represents all the HTML elements on your page. It's represented by a tree structure, where each element is a **node**. You've already seen the DOM when you look at the elements panel in dev tools!

JavaScript can find and modify any DOM node. Some things you might change with JavaScript:

- Update the text inside an element
- Add or remove a class to trigger CSS3 transitions
- Hide or show elements
- Add dynamic HTML to the page

## Expressions and values
A _value_ is a piece of data (more abstractly, a sequence of 0's and 1's).  
An _expression_ is any piece of code or instruction given to the computer that produces a value.

```js
//this is an expression
> 1 + 1
// this is the value produced by that expression
2
```
In the console, the value is returned immediately after you press enter.

Vocabulary is very important because it helps us ask coherent questions and adds structure to our thinking. Just as we learned **selector**, **rule**, **property** and **value** in CSS, so we will drill **expression** and **value** into your head now.

## Data types

Every JavaScript value has a _type_ which can determine where that value can be used. Here are some types you will encounter:

Data type | Description | Example
---|---|---
number | Integers & decimals/floats | `10`, `10.001`
string | Characters including spaces | `'internetUser993'` `"123 Main St."`
boolean | A reserved keyword that looks like an English word| `true`, `false`
undefined | Does not have a value | `undefined`
null | Has a value of nothing | `null`
object | A set of organized data | `{studentNumber:231, instructor:"Hyram Outke"}`

> There's also a (new in ES6) data type called Symbol but it's used mostly in library creation and you won't see it much.

If you want a mnemonic, some of our instructors like **SNUBON(S)**.

### typeof

There is a special operator we can use to check types called `typeof`. When used with a value it will tell us the type of that value. 

```js
typeof "HackerYou";
//string

typeof 3792
//number

typeof "a bunch of fibers rolled up together";
//string

```
## Pseudo code
When you're writing JavaScript (or other code) it can be helpful to map the detailed steps your program will carry out in plain English, just like we did in the alien exercise. This is called _pseudo code_ and it's a useful strategy for organizing your ideas about how a program should run without worrying about the language's syntax. It's like outlining an essay in point form before going back and writing the actual essay.

```json
when the user scrolls down the page:
* measure how far they've scrolled
* if they've scrolled more than 400px
  - show a tooltip
* otherwise
  - hide the tooltip
```

Every project you write should have pseudo code. We will often require it, so get into the habit of writing it now!
