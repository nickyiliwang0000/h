# This is your cohort's bulletin board! 
## Here is where we will post the weekly schedule, review topics for tests, and anything else we need you to know

### Schedule

Week 5: Deep in the wilds of JS

```
< Monday />
NO CLASS

< Tuesday /> 
DUE Project 3 
Kickoff
Stand-ups
Understanding API documentation
Art code-along
LUNCH
Project 3 presentations
Project 4 introduction
Project work time

< Wednesday /> 
Working with asynchronous events
Intro to Firebase
To-do app with Firebase code-along
SALAD CLUB
Project work time

< Thursday />
Class-based programming
LUNCH
Lexical scope and execution context
Project work time

< Friday />
JavaScript + jQuery test
Feedback form
Fetching data with something other than $.ajax
Destructuring, mutability, and purity
LUNCH
Project work time
Show 'n' Tell
```
<!-- ### Review topics -->

### Review topics for JavaScript + jQuery test (Friday May 24)
Objects and arrays 

Variable assignment and scope

Differences between the functional programming methods we learned

Arrow functions

Promises

### General feedback from the mock tech test

> Given the array below, how would you create a new array that holds **only** the names of the beaches with pictures?

🎉 Successes 🎉
* Lots of people know for loop syntax by heart. Woo!
* A couple people drew on the data to highlight what they _expected_ to get back. That's great! Know your data, know which ones you expect to get back, so you don't get a false positive for your filtering condition. (e.g. both beaches, or `Tyrell beach` and `Lowell forest`)
* Lots of people couldn't remember the syntax for what they wanted to do (totally okay!), but could explain the method they wanted and what it did (excellent!). 
* Lots of saying you're use `const` for the new array, which is great, because you don't have a reason for it to be a `let`.
* Lots of people correctly mentioning that `map` returns an array.

🔨 Things to work on 🔨
* If you only wrote code and you're not 1000000% sure your code works, **write some pseudo code**!
* A lot of people wrote code that returned `['Tyrell beach', 'Lowell forest']`, which would have been fine if all the locations were beaches. But they were not.
* A couple people mentioned jQuery, but remember: `map`, `filter`, and `forEach` (and `reduce`) are now native JS methods! 


The most concise way to solve this this problem is with `.filter()` **and** `.map()`:
```js
const locations = [
  {name:'Tyrell beach',
  type:'beach',
  img:'images/tyrellBeach.png'
  },
  {name:'Mo\'okai beach',
  type:'beach',
  },
  {name:'Lowell forest',
  type:'forest',
  img:'images/lowellForest.png'
  }
]

const beachesWithPicture = locations.filter(location =>{
  return location.type === 'beach' && location.img
}).map(beach =>{
  return beach.name
});
```

A more readable version breaks the return from the `.map` out into its own variable:
```js
const beachesWithPicture = locations.filter(location =>{
  return location.type === 'beach' && location.img
});

const beachNames = beachesWithPicture.map(beach =>{
  return beach.name
});
```

You could also use `.forEach`:
```js
const beachNames =[];

const beachesWithPicture = locations.forEach(location =>{
  if(location.type === 'beach' && location.img){
    beachNames.push(location.name)
  }
});

const beachNames = beachesWithPicture.map(beach =>{
  return beach.name
});
```

You could also use a `for` loop:
```js
const beachNames =[];
for(let i=0;i<locations.length;i++){
  if(locations[i].img && locations[i].type === 'beach'){
    beachNames.push(locations[i].name)
  }
}
```

Less preferred would be nested `if` statements inside that `for` loop:
```js
const beachNames =[];

for(let i=0;i<locations.length;i++){
  if (locations[i].img) {
    if(locations[i].type === 'beach'){
      beachNames.push(locations[i].name);
    }
  }
}

```
### Bootcamp calendar
We use [this](https://calendar.google.com/calendar/embed?src=hackeryou.com_ckj6930nr6kraakaisos09cccs%40group.calendar.google.com&ctz=America%2FToronto) Google Cal to post all important dates & events throughout the Bootcamp and beyond! All events and dates for your cohort will be denoted by "2019 Spring Bootcamp: (event)".

### Important links
Submission form: http://bit.ly/HYsubmissions

Feedback form: http://bit.ly/HYBootcampFeedback

Group assignments: https://docs.google.com/spreadsheets/d/1NxNPhvE2nyfkh1zwraA8YGM2SPIMXVm0PHSv430CCGw

