# This is your cohort's bulletin board! 
## Here is where we will post the weekly schedule, review topics for texts, and anything else we need you to know

### Schedule
Week 5: Deep in the wilds of JS and a React sighting...

< Monday />
- DUE Project 3 
- Stand-ups
- Understanding API documentation
- Art code-along
- 🍴LUNCH 🍴
- Project 3 presentations
- Project 4 introduction
- Project work time

< Tuesday /> 
- Working with asynchronous events
- 🍴LUNCH 🍴
- Intro to Firebase
- To-do app with Firebase code-along
- Project work time

< Wednesday /> 
- Class-based programming
- Lexical scope and execution context
- 🥗SALAD CLUB 🥗
- Career Services Presentation
- Destructuring 
- Project work time

< Thursday />
- Making our code more modular
- Intro to React
- 🍴LUNCH 🍴
- Breaking our apps into components
- Project work time

< Friday />
- JavaScript +jQuery test
- Feedback form
- Events in React
- 🍴LUNCH 🍴
- React Lifecycles
- Show ‘n’ Tell

### Study areas for JS/jQuery Test
- Objects
- Arrays
- Variable assignment and scope
- Difference between the functional programming methods we learned (map, filter, reduce, forEach)
- Arrow functions
- Promises (Tuesday lesson)


### Mock Test Feedback
> Given the array below, how would you create a new array that holds **only** the names of the beaches with pictures?

Many solutions to this one. One way would be a very concise chaining of `.filter()` **and** `.map()`:

```JS
const locations = [
  {
    name: "Tyrell beach",
    type: "beach",
    img: "images/tyrellBeach.png",
  },
  {
    name: "Mo'okai beach",
    type: "beach",
  },
  {
    name: "Lowell forest",
    type: "forest",
    img: "images/lowellForest.png",
  },
];

const newBeachesArray = locations
    .filter(location => {
      return location.img && location.type === "beach";
    })
    .map(beach => {
      return beach.name;
    });
```
A more readable version breaks the return from the `.map` out into its own variable:

```js
  const beachesWithPicture = locations.filter(location => {
    return location.type === 'beach' && location.img
  });
  const beachNames = beachesWithPicture.map(beach => {
    return beach.name
  });
```

Using `.forEach()`:

```js
const beachNames = [];

const beachesWithPicture = locations.forEach(location => {
  if (location.type === "beach" && location.img) {
    beachNames.push(location.name);
  }
});
```

Or, with a `for` loop:

```js
const beachNames =[];
for(let i=0; i < locations.length; i++) {
  if(locations[i].img && locations[i].type === 'beach'){
    beachNames.push(locations[i].name)
  }
}
```

🎉 Successes 🎉
* Lots of people know their JS method syntax by heart!
* Lots of people highlighted or made notations on the data provided. AWESOME! Know your data so you can make accurate conclusions.
* When you can't remember the specific syntax, it's still valuable to be able to explain the method you want to use or the logic behind the process. A lot of people did this so 👍👍
* Lots of people highlighted or made notations on the data provided. AWESOME! Know your data so you can make accurate conclusions.

🔨 Things to work on 🔨
* Make sure you are reading the instructions and your data carefully!! A few people wrote code that only returned the images and not the name. Some wrote code that returned `['Tyrell beach', 'Lowell forest']` which would be ok if all locations were beaches.



### Bootcamp calendar
We use [this](https://calendar.google.com/calendar/embed?src=hackeryou.com_ckj6930nr6kraakaisos09cccs%40group.calendar.google.com&ctz=America%2FToronto) Google Cal to post all important dates & events throughout the Bootcamp and beyond! All events and dates for your cohort will be denoted by "2019 Summer Bootcamp: (event)".

### Important links
Submission form: http://bit.ly/HYsubmissions

Feedback form: http://bit.ly/HYBootcampFeedback

Group assignments: [Here](https://docs.google.com/spreadsheets/d/126VVJAOeyEXjZrk_RDj7GUg0qqoAB5oNwJbYGhclymo/edit#gid=624584399)

