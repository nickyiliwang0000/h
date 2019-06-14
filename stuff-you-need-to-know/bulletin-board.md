# This is your cohort's bulletin board! 
## Here is where we will post the weekly schedule, review topics for texts, and anything else we need you to know

### Schedule


```bash
Week 8: The home stretch 

< Monday />
Kickoff
Stand-ups
Project Work Time
Blog Post #3 Due

< Tuesday />
Project Work Time
Lunch ‘n’ Learn - Career Planning with Miguel Bautista

< Wednesday />
DUE Project 6 - 10am
Project 6 presentations
Introduce final project
Group React project feedback form
LAST SALAD CLUB ;-;
Resume & Cover Letter Lesson
Project Clean-Up/Resume Work Time

< Thursday />
Project Clean-Up/Resume Work Time
Portfolio Theme Due for Approval
LUNCH
Soft Skills with Sarah & Charlotte
Extra-Curricular: Design Fishbowl - 6pm to 8pm

< Friday />
Mock Tech Test
Feedback Form
Week 9 (and beyond) Overview
Portfolio Work Time
Final Show ‘n’ Tell
```

Next Monday is your final exam. 25 multiple choiced questions covering everything we've learned. 

Specific review topics:

* HTML fundamentals
* CSS quirks (e.g. browser defaults, ghost space, resets,box-sizing, cross-browser inconsistencies, floats, etc.)
* JS syntax (e.g. arrow functions/other ways of declaring functions, template literals, let vs. const, variable scope, etc.)
* What modules are and how we use them
* React lifecycle methods
* State in React
* Complex and simple components
* Basic Firebase methods
* git commands
* Definitions including abbreviations (e.g. ECMAScript, AJAX, JSX etc.)


### Mock tech test feedback
> Given the following code:
>
>  ```js
>  const tool = "paintbrush";
>
> function makeArt() {
>    let tool = "pencil";
>    console.log(tool)
>  }
>
>  makeArt();
> ```
> What will be logged to the console? Why?

This is a tricky one meant to prep you for technical interview questions that are like "read this code without a computer and tell me what it does". (Personally, I don't think this is a great way to test whether you'll be able to do the job, but it _is_ a way to find gaps in your own knowledge about why things happen the way they do in JavaScript.)

The correct answer is `pencil`. Variables can have the same name as long as they are in different scopes in JavaScript. A fun quirk! 🙃

JavaScript sees two `tool` variables, one in the global scope and one in `makeArt`'s function scope. 

Remember how when a function is run (e.g. `console.log(tool)`), the JavaScript engine looks around for a variable called `tool` in the current execution context ? And if it doesn't find one, it looks for variables in the enclosing execution contexts until it finds one? 

The execution context for `console.log` is as follows:
| Item | Inventory |
| ---- | --------- |
|Variables |	tool (the one defined with `let`)|
|Functions |	_none_|
|Other scopes |	`makeArt`,`global execution context`|
| `this` | Reference to window|

The execution context for `makeArt` is as follows:
| Item | Inventory |
| ---- | --------- |
| Variables |	tool (the one defined with `const`)|
| Functions |	_none_|
| Scopes |	`global execution context`|
| `this` | Reference to window|

If there hadn't been a `tool` variable declared inside the `makeArt` scope, `console.log()` would have gone looking to the global execution context for `tool`. As it stands, `console.log()` finds what it needs and can perform its task without ever seeing know `const tool = "paintbrush"` exists.

Successes
* Lots and lots of people chose `pencil`!
* Lots of people mentioned that `const` can't be overwritten. Yes! Show your knowledge!
* Lots of people mentioned that one shouldn't have local and global variables with the same name.
* Lots of people correclty identified that if the `console.log` were to be run _outside_ of the `makeArt` function, they would get `paintbrush`.


* A good number of people said there'd be an error. Which there absolutely would be _if_ we were trying to redeclare `tool` with `let` in the same scope as `const tool` or if we omitted the `let` keyword all together inside the `makeArt` function. 


Check out the differences here:

```js
const tool = "paintbrush";

function makeArt() {
  tool = "pencil";
  console.log(tool)
}

makeArt();
// Error -  can't redeclare a const
```

```js
let tool = "paintbrush";

function makeArt() {
  tool = "pencil";
  console.log(tool)
}

makeArt();
// pencil
```

```js
const tool = "paintbrush";

function makeArt() {
  console.log(tool)
}

makeArt();
// paintbrush
```
 
### Bootcamp calendar
We use [this](https://calendar.google.com/calendar/embed?src=hackeryou.com_ckj6930nr6kraakaisos09cccs%40group.calendar.google.com&ctz=America%2FToronto) Google Cal to post all important dates & events throughout the Bootcamp and beyond! All events and dates for your cohort will be denoted by "2019 Spring Bootcamp: (event)".

### Important links
Submission form: http://bit.ly/HYsubmissions

Feedback form: http://bit.ly/HYBootcampFeedback

Group assignments: https://docs.google.com/spreadsheets/d/1NxNPhvE2nyfkh1zwraA8YGM2SPIMXVm0PHSv430CCGw

