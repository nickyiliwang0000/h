<!-- Student takeaway: -->
<!--Student will be able to:
- Understand what .map does
- Explain why you would use .map
- Refactor a section of code into a new component
-->

# Breaking our app into components

One of the tenets of efficient, modern programming is to avoid repeating yourself. This improves code maintainability, readability, and reusability, and decreases complication. The less complicated our code is, the easier bugs will be to track down and squash!

Code reusability is one of the huge benefits we gain from building our app using the React library. Our components can be reused across our project, which means less work for us (and fewer files to go through when bug hunting).

## How to break an app into components 
What does code reusability look like? Well, let's imagine that we're building an app for an animal shelter and we want to have a page that displays all of the pets that are available for adoption:

```javascript
// animals.js
const animals = [
  {
    name: 'Phoebe',
    type: 'dog',
    size: 'medium',
    picture: 'https://d17fnq9dkz9hgj.cloudfront.net/uploads/2018/04/Bulldog_02.jpg',
  },
  {
    name: 'Rajni',
    type: 'fish',
    size: 'small',
    picture: 'http://natgeo.petsmart.com/content/img/betta-fish/betta-fun-facts.jpg'
  },
  {
    name: 'Momo',
    type: 'dog',
    size: 'small',
    picture: 'https://upload.wikimedia.org/wikipedia/commons/thumb/7/7d/BostonTerrier001.JPG/220px-BostonTerrier001.JPG'
  }
];

export default animals;
```

```jsx
// App.js
import React, { Component } from 'react';
import animals from './animals.js';

class App extends Component {
  render() {
    return (
      <div>
        <h1>Adopt Us!</h1>
      </div>
    )
  }
}

```

Here we have created an `App` component and rendered it on to the page. We have also imported information about all our animals from a file called `animals.js`. In the real world this information might come from an API, but for now we're just storing it in a JS file.

So, how do we get this information on the page? Well, we could write something like this:

```jsx
// App.js
import React, { Component } from 'react';
import animals from './animals';

class App extends Component {
    render(){
    return (
      <div>
        <h1>Adopt Us!</h1>
        <div className="pet">
          <h2>{animals[0].name}</h2>
          <p>Type: {animals[0].type}</p>
          <p>Size: {animals[0].size}</p>
          <img src={animals[0].picture} alt={`An adorable ${animals[0].type}.`} />
        </div>
        <div className="pet">
          <h2>{animals[1].name}</h2>
          <p>Type: {animals[1].type}</p>
          <p>Size: {animals[1].size}</p>
          <img src={animals[1].picture} alt={`An adorable ${animals[1].type}.`}/>
        </div>
        // another .pet div for every pet ...
      </div>
    )
  }
}
```

As you can see, we have to repeat the `div.pet` element for every animal inside of our `animals` array. This totally works, but requires writing a ton of repetitive code!

## Your new best friend in React: `.map()`
JavaScript to the rescue! In the past, when we have wanted to iterate over a bunch of items inside of an array and do something to them, what did we use? `.map()`! (Okay, we used a `for` loop or the .forEach() method sometimes, but in React we're going to stick with `map()`.)

Looping over items to do stuff to them works just as well in React as it did in jQuery. Remember that inside of JSX we can write any vanilla JS we want by escaping it with curly brackets `{}`. We can add a `.map()` right inside the `render` method and have it print out all of our animals!

Let's refactor our JSX to incorporate a `.map()` instead of manually typing out JSX for each animal:

```jsx
// App.js
import React, { Component } from 'react';
import animals from './animals';

class App extends Component {
  render() {
    return (
      <div>
        {animals.map((animal) => {
          return (
            <div>
              <h2>{animal.name}</h2>
              <p>Type: {animal.type}</p>
              <p>Size: {animal.size}</p>
              <img src={animal.picture} alt={`An adorable ${animal.type}`}/>
            </div>
          )
        })}
      </div>
    )
  }
}
```

Now let's imagine for a minute that our app is starting to get a lot bigger, and the section that features our list of animals for adoption is only one part of a larger page:

```jsx
//App.js
import React, { Component } from 'react';
import animals from './animals.js';

class App extends Component {
  render() {
    return (
      <div>
        <h1>Adopt a Pet!</h1>
        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>

        <h2>About our Pets</h2>
        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>

        <h3>Animals Featured for Adoption</h3>
        <div>
          {animals.map((animal) => {
              return (
                <div>
                  <h2>{animal.name}</h2>
                  <p>Type: {animal.type}</p>
                  <p>Size: {animal.size}</p>
                  <img src={animal.picture} alt={`An adorable ${animal.type}`}/>
                </div>
              )
            })}
        </div>
      </div>
    )
  }
}
```

This creates two issues:
1. When we want to work on the "Animals Featured for Adoption" section, we have to dig a bit through our `App` component in order to find that section.
2. What happens if we want to feature our pets in different parts of our app? We'd have to copy this code and paste it somewhere else. This isn't good because then if we need to change it, we have to change it in **_both_** places!

## Importing a component 
So what can we do? Let's create a `PetList` component to hold the JSX information about all of our pets. That way, anywhere we need to print this information to the page, we'll be able to reference it by typing `<PetList />`.

```jsx
//PetList.js
import React, { Component } from 'react';
import animals from './animals';

class PetList extends Component {
  render() {
    return (
      <div>
        {animals.map((animal) => {
          return (
            <div>
              <h2>{animal.name}</h2>
              <p>Type: {animal.type}</p>
              <p>Size: {animal.size}</p>
              <img src={animal.picture} alt={`An adorable ${animal.type}`}/>
            </div>
          )
        })}
      </div>
    )
  }
}

export default PetList;
```
> Don't forget to import `animals` to this new PetList file instead of the App.js file!

Now we have a `PetList` component that we can use anywhere to print out our list of pets! Let's refactor our `App` component to bring in our `PetList` component:

```jsx
//App.js
import React, { Component } from 'react';
import PetList from './PetList.js';

class App extends Component {
  render() {
    return (
      <div>
        <h1>Adopt a Pet!</h1>
        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>

        <h2>About our Pets</h2>
        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>

        <h3>Some of our animals featured for adoption</h3>
        <div>
          <PetList />
        </div>
      </div>
    )
  }
}
```
> Don't forget to import `PetList` at the top!

By breaking `PetList` into its own component, we have made our code more modular, more readable, and more maintainable!

## Wrapping up
As you start building your own apps, notice when you're re-writing a lot of the same code over and over again. If you are, ask yourself: could this be refactored into a separate component? Sometimes it's only a line or two and the tradeoff isn't worth it, but very often breaking your app into smaller components will make it easier for you (and other developers) to keep track of what's going on!
