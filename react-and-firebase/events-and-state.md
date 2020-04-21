# Events and state

An _event_ is an interaction with the DOM by the user. We should be somewhat familiar with events from our time with jQuery. 

In JavaScript, when you're thinking about an event, you're usually thinking about two things:
1. the event itself (e.g. a user clicks a button).
2. the event handler (i.e. the code that runs when the user clicks the button).

In jQuery, we handled events like this:

```javascript
$('button').on('click', function(){
  // some event handler code we would like to run when the button is clicked
});
```

In React, things work a little bit differently. First we begin by attaching our event handler to the DOM element of choice like this:

```jsx
class Button extends Component {
  render() {
    return (
      <button onClick={this.handleClick}>Add to cart</button>
    )
  }
}
```
The `this` keyword represents our `Button` component so we can think of our `handleClick` method as a property attached to the `Button` class. Then we write an event handler method inside of our component that describes what we want to happen when the button is clicked.

```jsx
class Button extends Component {

  handleClick(){
    alert("Item added to the shopping cart!");
  }

  render() {
    return (
      <button onClick={this.handleClick}>Add to cart</button>
    )
  }
}
```

## State in React

_State_ describes the part of an application that changes over time.

Think about your Netflix account. At any given point, you're either logged in or you're not logged in. Netflix needs to know which one is true so that you can either be shown the login screen or your personal profile.

Information about your login status is stored inside of the **state** of the Netflix application.

So somewhere, nestled in the codebase of Netflix, there's probably an object that looks like this:

```javascript
  user = {
    loggedIn: false
  }
```

When you log in, `user.loggedIn` is set to `true`. Your action of logging in changed the state of the application.

In React, each one of your components can have it's own state, where it can store information that is relevant to that particular component.

For example, let's imagine it's 1995 and we want to have a sweet visitor counter to keep track of how many people have been to our page.

```jsx
class Counter extends Component {
  render() {
    return (
      <div>
        <p>You are visitor number 57.</p>
      </div>
    )
  }
}
```

Let's imagine that we have some mechanism that can keep track of how many people have visited our page. As people visit the site, the number 57 is going to need to be updated (i.e. it is the part of our application that changes over time). This is a sign that it's a good candidate to be stored in state.

Here's how we would move the information about our visitors into our state:

```jsx
class Counter extends Component {
  // The constructor allows us to set default properties, such as the state, of our new component.
  // Note that when using the extends keyword, the super method is required to gain access the special stuff that comes with being a React Component
  constructor() {
    super();
    this.state = {
      visitors: 0
    }
  }

  render() {
    return (
      <div>
        {/* anything inside curly brackets is vanilla JavaScript - here we are accessing the `state` object on the `Counter` component, and printing out the value of the `visitors` property on to the page. */}
        <p>You are visitor number {this.state.visitors}.</p>
      </div>
    )
  }
}
```

In this case `this.state.visitors` behaves a bit like if we had declared `let visitors = 0` as a global variable in vanilla JS; it would display the text as `You are visitor number 0.` If we updated that `visitors` variable to `1` and reloaded the page, the text would then read `You are visitor number 1.`

State in React works similarly to this, except it functions asynchronously, so if we update state, then it will re-render our text with the updated number without needing to reload the page.


## Combining events and state

Now that we have an understanding how state and events work, let's combine them to build a simple counter mechanism that can count up from 0.

We'll start by creating our `Counter` class:
```jsx
class Counter extends Component {
  render() {
    return (
      <div>
        <p>I am currently on number: 0</p>
        <button>Increment</button>
      </div>
    )
  }
}
```

Cool! We know that the number `0` is going to need to change over time (as the counter increments it), so let's move it over into the state:

```jsx
class Counter extends Component {
  constructor() {
    super();
    this.state = {
      count: 0
    }
  }

  render() {
    return (
      <div>
        <p>I am currently on number: {this.state.count}</p>
        <button>Increment</button>
      </div>
    )
  }
}
```

Here we've created a `count` property in our `state` object, which we set inside our constructor. Then instead of printing out the number `0`, we use `this.state.count` to print out whatever the current value of the count is.

> Try modifying the value of `this.state.visitors` inside the constructor - you'll notice that the change is reflected when we refresh the page!

### Using events to change state
Now let's make it so that we can increment the counter when the button gets clicked.

Let's start by attaching an event listener to the button:

```jsx
render() {
  return (
    <div>
      <p>I am currently on number: {this.state.count}</p>
      <button onClick={this.handleClick}>Increment</button>
    </div>
  )
}
```

We add the `onClick` attribute to the button and set it to be equal to a function called `this.handleClick`. Let's create that function now, and let's `console.log()` our state to see that we have access to it:

```jsx
class Counter extends Component {
  constructor() {
    super();
    this.state = {
      count: 0
    }
  }

  handleClick() {
    console.log(`The current state is ${this.state.count}!`);
  }

  render() {
    return (
      <div>
        <p>I am currently on number: {this.state.count}</p>
        <button onClick={this.handleClick}>Increment</button>
      </div>
    )
  }
}
```

There's a problem though. When we try running our code and clicking our button, we get an error:

```bash
Error! `TypeError: this is undefined [Learn more]`
```

It looks like the value of `this` is `undefined` inside of our `handleClick` method!

This is a particular quirk of JavaScript where the `this` value isn't bound when `handleClick` is called. Before, we could solve this issue by binding our methods to the component instance within our `constructor`:

```jsx
class Counter extends Component {
  constructor() {
  super();
  this.state = {
    count: 0
  }
  this.handleClick = this.handleClick.bind(this);
}
```

While you still may see this approach done in the wild or in legacy code, we will instead change how we define our method - we use an arrow function:

```jsx
// We start by declaring our new `Counter` component.
class Counter extends Component {
// In its constructor, we set the initial state of the component to include a `count` property with a value of 0.
  constructor() {
    super();
    this.state = {
      count: 0
    }
  }

  handleClick = () => {
    console.log(`The current state is ${this.state.count}!`);
  }

  render() {
    return (
      <div>
        <p>I am currently on number: {this.state.count}</p>
        {/* Added a event listener by adding an `onClick` attribute and passing in the `handleClick` method as its value. When the increment counter button is clicked, `this.handleClick` is called */}
        <button onClick={this.handleClick}>Increment counter!</button>
      </div>
    )
  }
}
```

Since we are using arrow functions our event handler is automatically bound to the component instance, so we do not need to worry about binding it in the constructor. Try clicking your button again, and you should get the console log as we initially expected. Great!

Next, instead of logging our current state to the console, we will update that state in our `handleClick` function:

```jsx
class Counter extends Component {
  constructor() {
    super();
    this.state = {
      count: 0
    }
  }

  handleClick = () => {
    this.setState({
      count: this.state.count + 1
    })
  }

  render() {
    return (
      <div>
        <p>I am currently on number: {this.state.count}</p>
        <button onClick={this.handleClick}>Increment</button>
      </div>
    )
  }
}
```

Inside of `handleClick`, you'll notice we're calling a method you haven't seen before: the `setState` method. `setState` is a React method which allows us to update the current state of our application by passing in an object containing the piece of state we want to update. In React, this is how we always want to update our state, as opposed to directly altering state. We will explore this more in a later lesson.

Since we want to update `this.state.count`, we pass in an object with a key of `count` and a value of what we want to update `count` to. In this case, we want to set it to what it was before, plus one.

Now you'll notice that every time you click the increment button, the number on the page increases! This is because every time `setState` is called, our component _rerenders_, which basically means it refreshes itself and grabs the most up-to-date state information.

And that's all there is to it! `onClick` is one of many different events that React can handle - there's also `onMouseOver`, `onMouseDown` etc. - [check out the React docs for the full list](https://facebook.github.io/react/docs/events.html).

### Conditional rendering and ternary operators

Often, we want to reflect state changes in our application conditionally. For example, maybe we want to show a welcome message only once a user logs into our page.

You may be tempted to put an `if` statement in your JSX like this:

```jsx
render() {
  return (
    <div>
      {if(userIsLoggedIn) {
        <h1>Welcome, friend!</h1>
      }}
    </div>
  )
}
```

This would throw an error though; a gotcha with React is that the JavaScript you put inside of JSX has to return something. This means that anything inside of curly brackets `{}` in the `return()` has to be an expression, and `if` statements are **statements**, not expressions.

Luckily for our dynamic React content, there are a few ways to get around this, including using _[ternary operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)_ for conditional rendering.

The syntax for a ternary is: 

`condition ? true : false`

Think of the `?` as the `if` and the `:` as the `else` in a conditional statement.

```jsx
render() {
  return (
    <div>
      {userIsLoggedIn ? <h1>Welcome, friend!</h1> : null}
    </div>
  )
}
```

The code above is saying: if the variable `userIsLoggedIn` is `true`, return the `h1` tag, otherwise return `null`. 
    
Using ternary operators to conditionally render content can get messy pretty quickly, so it is also common to use functions or variables outside of the `return()` to accomplish this:

```jsx
render() {
  let markupShowingOnPage = null;

  if (userIsLoggedIn) {
    markupShowingOnPage = `<h1>Welcome, friend!</h1>`;
  }

  return (
    <div>
      {markupShowingOnPage}
    </div>
  )
}
```

You can find more information on conditional rendering in the [React docs](https://reactjs.org/docs/conditional-rendering.html).
