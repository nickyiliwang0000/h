# This is your cohort's bulletin board! 
## Here is where we will post the weekly schedule, review topics for texts, and anything else we need you to know

### Schedule
Week 7:  A taste of some cool tools to explore 

< Monday />
* Kickoff
* Stand-ups
* Project work time
* 🍴LUNCH 🍴
* Git Collab Cont’d
* Project work time

< Tuesday />
* Project work time
* DUE Project 5 
* 🍴LUNCH 🍴(Accessibility Lunch n Learn w/Jen Taylor)
* Project 5 Presentations
* Introduce Project 6
* Project work time

< Wednesday />
* Routing
* Hackflix code-along
* 🥗SALAD CLUB 🥗
* Project work time

< Thursday />
* Unspecified group activity
* Project work time
* 🍴LUNCH 🍴
* Extra React code-along
* Project work time

< Friday />
* React test
* Feedback form
* Project work time
* 🍴LUNCH 🍴
* Project work time
* Show ‘n’ Tell



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

