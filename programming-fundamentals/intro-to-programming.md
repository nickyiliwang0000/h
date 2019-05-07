<!-- Student takeaway: -->
<!--Student will be able to:
- What a programming language is (as opposed to a style sheet language or a markup language)
- That syntax is important
-->

# Intro to programming
*A programmer's partner sends them to the grocery store with instructions: "Get a litre of milk. If they have eggs, get a dozen."*

*The programmer comes home a short while later with an armful of milk cartons.*

*"Why did you get so much milk?" the programmer's flabbergasted partner asks.*

*The programmer replies, "They had eggs."*

## A quick primer on programming languages

So far, we've created our projects using HTML (a markup language) and CSS (a style sheet language). These languages have have allowed us to add content to and style our web pages. If we want our web pages to do other things, things like responding to events, communicating with services, or modifying styles on the fly, we need to have a deeper conversation with the computer. 

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

As with learning a new spoken language, the best way to learn programming is real-world practice with a native speaker. To do this in programming, it helps to **think like a computer**. Human spoken language has rhyme, tone, irony, humour, homophony, and onomatopoeia to convey meaning; most programming languages do not. So, we have to be much more explicit in programming than in English; we have to break instructions into very small steps when speaking a computer's language.

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

In small groups, write out detailed step-by-step instructions for how to make an apple pie from scratch. We'll compare your answers together to see just how specific you can get!

### Invent the world, maybe
There's a quote attributed to Carl Sagan that goes: 
>In order to make an apple pie from scratch, you must first invent the universe.

While it's not true that you have to invent the universe every time you make a new website, even simple-seeming programs can require many, many steps to complete.

