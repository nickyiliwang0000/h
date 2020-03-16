## JavaScript fundamentals exercises

Time to combine all the fundamentals we've used so far and used them together to built a small JavaScript program.

Remember to break down your program into small steps that a computer can understand. Write out some pseudocode first and refer to this [JavaScript Cheat Sheet](https://github.com/HackerYou/bootcamp-notes/blob/master/stuff-you-need-to-know/resources-and-cheat-sheets/javascript-cheat-sheet.md) help you with the syntax as you translate pseudocode into JavaScript.

## Coin flip
We'll build a JavaScript coin flipping machine! Open up [js-fundamentals-exercise](https://hychalknotes.s3.amazonaws.com/js-fundamentals-exercise.html) to get started. Download [js-fundamentals-exercise-ANSWER](https://hychalknotes.s3.amazonaws.com/js-fundamentals-exercise-ANSWER.html) if you get stuck.

## Create a Mad Libs game
This exercise was created by bootcamp grad Garret Levine!
1. Prompt the user for 3 seperate words:
  * A noun
  * An adjective
  * An adverb
2. Using these choices, `console.log` a Mad Lib where the prompts replace the blanks...
``` bash
"After they did that, the king played chess on his brother's
__________(noun) and then combed his __________ (adjective)
hair with a comb made out of old fish bones.
Later, that same day, I saw the Monkey King dance __________
(adverb) in front of an audience of kangaroos and wombats."
```
3. Instead of always printing that Mad Lib, have your program randombly choose that one or this one:

```bash
"The day I saw the Monkey King
__________(adverb) sing. It was one of the most
__________(adjective) days of the year.
Everyone brought their _________(noun) and was havin a great time!"
```

You will need to:
  * store each Mad Lib template in a variable 
  * get a random number between 1 and 2 (look at using `Math` in JavaScript)
  * `console.log` a different Mad Lib depending on the number returned from the `Math` method you choose.





## Calculator

1. Create a program that acts as a calculator. Have functions `add` `subtract` `multiply`, etc. Functions should take in 2 or more values and return the result of that operation. 

2. Create functions for more complex functions: calculating circumference given radius, using the quadratic formula, calculating cosine, sine, and tangent (without the `Math.` methods!)



