# This is your cohort's bulletin board! 
## Here is where we will post the weekly schedule, review topics for texts, and anything else we need you to know

### Schedule
Week 4: jQuery && JavaScript

< Monday /> 
* Kickoff
* Stand-ups
* Spread, Rest and Destructuring
* Project 4 Presentations
* Project 4 Introduction
* 🍴LUNCH 🍴
* Understanding API Documentation
* Code Along: Rijksmuseum API art


< Tuesday /> 
* Working with Asyncronus Events
* Intro to Firebase
* 🍴 LUNCH 🍴 (Accessibility Lunch and Learn with Jen Taylor)
* Firebase Code-along
* Project work time (PJWT)


< Wednesday /> 
* Class Based Programming
* Lexical Scope and Execution Context
* 🥗SALAD CLUB 🥗
* Career Services Presentation
* Project work time (PJWT)


< Thursday /> 
* Project work time (PJWT)
* 🍴LUNCH 🍴 
* Project work time (PJWT)


< Friday />
* _Javascript/Jquery Test_
* Making our Code Modular
* Intro to React
* 🍴LUNCH 🍴
* Breaking our app into Components
* Show ‘n’ Tell

### Mock Test Feedback
> Given the object below, how would you go about finding the key that has the highest value?
```JS
        let locations = {
            park: 10,
            forest: 1,
            mountains: 14,
            beach: 4,
            indoors: 7
        }
```
There are a couple of ways to do this! However the first option is the most performant.

```JS
        // OPTION 1 - *BEST PERFOMANCE* A For Each Loop and an External Variable 
        let largest = {key: '', number: 0};

        for(let key in locations){
            if (locations[key] > largest.number){
                largest.key = key;
                largest.number = locations[key];
            }
        }
        console.log(largest.key)

        //OPTION 2 - Sorting an Array

        const arrayOLocations = [];

        for(let key in locations){
            if (locations[key] > largest.number){
                const locale = {
                    key: key,
                    number: locations[key];
                }
                arrayOLocations.push(locale)
            }
        }

        arrayOLocations.sort((a, b) => {
            if(a.number > b.number){
                return 1;
            } else{
                return -1;
            }
        };

        console.log(arrayOLocations[0].key);
```

🎉 Successes 🎉
* Lots of people talked about checking the data type of the value using parseInt()
* Lots of people highlighted or made notations on the data and instructions provided. AWESOME! It makes it easier to refer back to what you are trying to accomplish.
* When you can't remember the specific syntax, it's still valuable to be able to explain the logic you want to use. You can also mention the syntax or method that you would look up in that situation. A lot of people did this so 👍👍
* Great combination of pseudo code and real code. 


🔨 Things to work on 🔨
* Make sure that you 👏 READ 👏 THE 👏 INSTRUCTIONS 👏 carefully!! A lot of people returned the highest value (14) rather than the _key_ of the highest value (mountains).
* It helps me to think about what I would console.log() when I get stuck whiteboarding and what would be the expected outcome of that variable. For example - I might start by looping over my object with a 'for each' loop. 
Once I get inside the loop feel unsure of the next steps, I pretend to `console.log(key)` so I can think about what I expect the console to output and I would realized that I actually needed to grab `object[key]`.
* The next step is to think about edge cases and performance in questions like these. What if the object had 2 of the same values? Would your solution still work? How would you choose between the two keys? What other edge cases can you think of? What is the array or object was thousands of entries long. This is the beginning of testing your code which is a subject that a lot of employers are passionate about. 



### Bootcamp calendar
We use [this](https://calendar.google.com/calendar/embed?src=hackeryou.com_ckj6930nr6kraakaisos09cccs%40group.calendar.google.com&ctz=America%2FToronto) Google Cal to post all important dates & events throughout the Bootcamp and beyond! All events and dates for your cohort will be denoted by "2019 Fall Bootcamp - (event)".

### Important links
Submission form: http://bit.ly/HYsubmissions

Feedback form: https://forms.gle/g9f6G8LB5FfJZFSF6

Group assignments: [Here](https://docs.google.com/spreadsheets/d/12P9pcvsRTf7Qek_FYETltPLghetwuyy5epxRaxqRns4/edit#gid=1112317742)

