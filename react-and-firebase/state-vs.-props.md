# State vs. props

In our previous lesson on state, we saw how information can be stored inside of a component using `this.state`. Storing data this way is useful when we're receiving that data from an external source or updating our component after a user has interacted with it (like incrementing a counter when a user clicks on it).

Sometimes we want to pass information from a parent component to child component in order to customize the way that child component renders. For this, we can use _props_ (short for _properties_).

Think about props as the options or configuration settings for a specific component. Props are one-time pieces of information that determine what the component should look like when it renders.

## An example of props: Toronto parks

Let's reopen our first-ever React app, the one with the `Welcome to the Toronto Parks' website`
 header. Imagine we're building an application for the city that shows off our city parks. Every week, a different one of the parks is featured.

We might make a component that looks like this:

```jsx
class FeaturedPark extends Component {
  render() {
    return (
      <h2>This week's featured park is: Sunnybrook</h2>
    ) 
  }
}

class App extends Component {
  render() {
    return (
      <FeaturedPark />
    ) 
  }
}
```

## Customizing our component with props

People LOVE the featured park. They flock to it in droves. In fact, it's getting so busy that the city decides to feature **three** parks to spread the traffic around. 

We could modify the JSX inside our `FeaturedPark` component to include the other two featured parks, but what happens if elsewhere on the site they only want to feature one park, not three, or a completely different set of parks? 

Let's create the ability to customize our `FeaturedPark` component to display any park depending on what options (a.k.a. props) we provide to it!

```jsx
class App extends Component {
  render() {
    return (
      <div>
        <FeaturedPark name="Sunnybrook" />
        <FeaturedPark name="Trinity Bellwoods" />
        <FeaturedPark name="Cherry Beach" />
      </div>
    );
  }
}
```

Any attribute value that we give to our `FeaturedPark` component will become accessible within the `FeaturedPark` component through `this.props`.

This means that we can change our `FeaturedPark` component to look like this:

```jsx
class FeaturedPark extends Component {
  render() {
    return (
      <h2>This week's featured park is: {this.props.name}</h2>
    )
  }
}
```

Now let's imagine that the city is demolishing condos to make room for more parks. Let's pretend we've already grabbed this information and it's stored in our state like so:

```jsx
class FeaturedPark extends Component {
  render() {
    return (
      <h1>This week's featured park is: {this.props.name}</h1>;
    ) 
  }
}

class App extends Component {
  constructor() {
    super();
    this.state = {
      featuredParks: ["Sunnybrook", "Trinity Bellwoods", "Cherry Beach"]
    };
  }

  render() {
    return (
      <FeaturedPark name="Sunnybrook" />
    ) 
  }
}
```

We can use `map` to loop through `this.state.featuredParks` and feed the name of each individual park to our `FeaturedPark` component as a prop. Then, we can return all the featured parks to the page like this:

```jsx
class App extends Component {
  constructor() {
    super();
    this.state = {
      featuredParks: ["Sunnybrook", "Trinity Bellwoods", "Cherry Beach"]
    };
  }

  render() {
    return (
      <div>
        {this.state.featuredParks.map((parkName, index) => {
          return <FeaturedPark name={parkName} index={index}/>;
        })}
      </div>
    );
  }
}
```

This way, in the future, as the city builds more parks, their names will get added to the state (i.e. the city's featured park database)and our `App` component will automatically render all the featured parks to the page!

**PRO TIP:** If you're ever unsure what's going to be in `this.props`, just `console.log` it out in your render function! (You can also find it in your React dev tools!)

## Passing functions as props

Let's create a new function within our `<App />` and name it `removePark`. We will use it to clear our `featuredParks` state. We will attach this function to a button element inside the`<FeaturedPark />` component. To gain access to the function inside `<FeaturedPark />` component, we need to pass a reference to it as a prop:

```jsx
  removePark = () => {
    this.setState({
      featuredParks: []
    })
  };

  render() {
    return (
      <div>
        {this.state.featuredParks.map((parkName, index) => {
          return <FeaturedPark removePark={this.removePark} name={parkName} index={index}/>;
        })}
      </div>
    );
  }
}
```

```jsx
class FeaturedPark extends Component {
  render() {
    return (
      <div>
        <h2>This week's featured park is: {this.props.name}</h2>
        <button onClick={this.props.removePark}>Remove park</button>
      </div>
    );
  }
}
```

### Passing functions with parameters

Our `<FeaturedPark />` component is successfully updating state in the parent `<App />` component! However, it makes more sense for each button to clear only the park it's attached to from the App's state. Since we are mapping through our state of featured parks, we can pass the index value as a parameter to our `removePark` function. This will force us to change how we pass `removePark` as a prop:

```jsx
class App extends Component {
  constructor() {
    super();
    this.state = {
      featuredParks: ["Sunnybrook", "Trinity Bellwoods", "Cherry Beach"]
    };
  }

  removePark = index => {
    // create a new array from the featuredParks in state
    const oldParks = [...this.state.featuredParks];
    
    // go through the oldParks array checking the index of the item to be removed 
    // against the iterator for this filter method
    // if the index of the item to be removed is NOT equal to the iterator for this filter method, 
    // put it in the updatedFeaturedParks array
    // otherwise, if the index is the same as the iterator, get rid of that entry
    const updatedFeaturedParks = oldParks.filter((name, i) => i !== index);
    
    // filter returns a new array, so we can use the return from the filter method to update our app's state
    this.setState({
      featuredParks: updatedfeaturedParks
    });
  };

  render() {
    return (
      <div className="App">
        {this.state.featuredParks.map((parkName, index) => {
          return (
            // here, we're asking the removePark function inside FeaturedPark 
            // to only run when the button is clicked
            // this way, we can include an argument
            <FeaturedPark
              removePark={() => this.removePark(index)}
              name={parkName}
            />
          );
        })}
      </div>
    );
  }
}
```

## Props and destructuring

So far our components have been fairly lightweight with only a few props. This won't always be the case. When we have lots of props, we can take advantage of object destructuring to help improve our component readability. Let's imagine that our props object looks like the following:

```js
const props = {
  author: {
    name: "Margaret Atwood",
    location: {
      city: "Toronto",
      province: "Ontario"
    }
  },
  review: "Really good at writing books.",
  date: "January 14, 1988"
};
```

```jsx
class AuthorDetails extends Component {
  render(){
    return (
      <div>
        <h1>{this.props.author.name}</h1>
        <h2>{this.props.author.location.city}</h2>
        <p>{this.props.review}</p>
      </div>
    );
  }
};
```

We can destructure our props within the `render()` method:

```jsx
class AuthorDetails extends Component {
  render(){
    const { author, review } = this.props;
    
    return (
      <div>
        <h1>{author.name}</h1>
        <h2>{author.location.city}</h2>
        <p>{review}</p>
      </div>
    );
  }
};
```

## So what's the difference between state and props?

When you're first starting to build React applications and you need to handle data inside a component, it's often hard to tell whether you should be using props or state.

Here are a few guidelines that can help you determine which one you need to use:

- Props are always passed down from a parent component to its child: they help the child determine what it should look like
- A component **cannot** modify props that it has received. So if your component has some piece of data that you know is going to need to be updated over time, then it probably makes more sense for it to be state.
- If you're handling some kind of user interaction (like a click event, for example), chances are you'll store that information in state.

Some of you may find this rudimentary flowchart helpful:
![state and props flowchart](https://hychalknotes.s3.amazonaws.com/state-props-flowchart-2018.png)

## Bonus 🎉

### Proptypes

As apps grow in scale, it is valuable to start thinking about how we can better improve the quality of our code to help prevent bugs. One way we can achieve this is to validate the types of data (e.g. strings, numbers, etc) that we pass to our components through props. If the data type that is passed through props is not what the component expects, a warning will be thrown to the console.

We can use the Proptypes library to do this kind of typechecking in React. To use it, we need to install it as a dependency in our app:

```javascript
npm install --save prop-types
```

After importing the Proptypes library, we can declare the expected data types for all the props in our component. Conventionally, this is written at the bottom of the component file, outside of its declaration:

```jsx
import React, { Component } from "react";
import PropTypes from "prop-types";

class Greeting extends Component {
  render() {
    return (
      <div>
        <h1>Hello, {this.props.name} you are the {this.props.visitorCount} visitor to this website!</h1>
      <div>
    )
  }
}

Greeting.propTypes = {
  name: PropTypes.string,
  visitorCount: PropTypes.number,
};
```

We are declaring that the `name` prop is expecting only a value with a typeof string and the `visitorCount` a value with a typeof number. Therefore, if we tried to pass a number to our `name` prop, we would get the following error:

`Warning: Failed prop type: Invalid prop 'name' of type 'number' supplied to 'Greeting', expected 'string'.`

For performance reasons, this validation only takes place in development mode and will not take place in a production environment. You can find a thorough list of the provided proptypes in the official React documentation, plus some additional features like setting default prop values.

## Additional Resources

- [React Docs on Props vs. State](https://facebook.github.io/react/docs/state-and-lifecycle.html)
- [Exploring State Management in React](https://hackeryou.com/blog/exploring-state-management-in-react)
- [React Destructuring Techniques](https://hackeryou.com/blog/react-destructuring-techniques)
- [Props vs. State](https://github.com/uberVU/react-guide/blob/master/props-vs-state.md) by the team at UberVU
