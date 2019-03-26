<!-- Student takeaway: -->
<!--Student will be able to:
- Know the difference between mounting and unmounting to the DOM
- Name four useful lifecycle methods (constructor, render, componentDidMount)
- Know which lifecycle methods are called when a component is mounted to the DOM (constructor, render, componentDidMount)
 -->

# The React component lifecycle

When we talk about the lifespan of a human, we talk about the stages of their life: childhood, adolescence, adulthood, old age. Well, just like humans, React components have their own lifespan, called a _lifecycle_.

And just like the stages in a human's life, React components have stages called _lifecycle methods_.

## What are the lifecycle methods?
Sometimes, you will find you need to perform a little bit of business before you're ready for your component to render on the page. Maybe you'd like to make sure you have a piece of data that you're retrieving from an API, or you'd like to make sure a user is authenticated to view the page that they've requested. Lifecycle methods can help you do that.

Lifecycle methods allow you to intervene at various stages of a React component's lifecycle (i.e. during its its creation/birth, updating/life, and destruction/death), in order to perform some kind of action. Since you don't have direct access to the React codebase, these lifecycle methods offer an opportunity for you to interact with and inject your own code into what would otherwise be a black box.

When a method allows you to intervene in the process of an existing piece of code, it is often called a _hook_.

### Mounting and unmounting
Let's start with a bit of terminology.

Whenever a React component gets added to the DOM, it's called _mounting_. We say that the component successfully _mounted_ to the DOM. 

When a React component is removed from the DOM, it's called _unmounting_. We say that that component successfully _unmounted_.

There are many React lifecycle methods (see [The Component Lifecycle](https://facebook.github.io/react/docs/react-component.html), visualized here:

![react component lifecycle methods](https://hychalknotes.s3.amazonaws.com/react-lifecycle-diagram.jpg)

You don't need to know all of these methods, especially when first starting out. We're going to focus on some of the most important and commonly used ones. 

When a component is mounted to the DOM, three lifecycle methods are called:

* **constructor()** - This is where you do things like set initial state and bind any functions to your component.
* **render()** - This is where you determine what gets displayed to the page.
* **componentDidMount()** - This is where you do things like make AJAX requests for data you'd like to use in your component.

When a component updates because its state or prop values were changed, this lifecycle method is called:

* **componentDidUpdate()** - This is where you can operate on the DOM and make network requests. **Note:** Actions performed here typically need to be wrapped in a condition to prevent an infinite loop. The documentation has more information [here](https://reactjs.org/docs/react-component.html#componentdidupdate).

When a component is unmounted from the DOM, the only one lifecycle method is called:
* **componentWillUnmount()** This is where you stop any recurrent logic associated with that component (like a timer or a recurring API call).

## Using the lifecycle methods
Hooking in to the lifecycle methods is very straightforward - we've actually already done it with both `render()` and `constructor()`! 

In order to access the lifecycle methods, simply reference them inside of your component:

```javascript
class App extends Component {
  constructor() {
    // here is our constructor lifecycle method
  }

  componentDidMount() {
    //  invoked immediately after a component is mounted
  }

  componentDidUpdate() {
    // here is anything we want to happen when a component is updated like when props or state change
  }

  componentDidMount() {
    // here is anything we want to happen after the component renders - like grab our AJAX data
  }

  render() {
    // here is any DOM elements we want to display on the page
  }
}
```

## Code-along: Art again!
We're going to use React, AJAX, Rijksmuseum API, and the lifecycle methods to build a little art gallery.

### Additional resources
* [The React Lifecycle Methods](https://reactjs.org/docs/react-component.html) - straight from the React docs.
* [Understanding the React Component Lifecycle](http://busypeoples.github.io/post/react-component-lifecycle/) - A. Sharif breaks down the React component lifecycle.