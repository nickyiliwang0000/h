# Props, and how they differ from state in React

In our previous lesson on state, we saw how information can be stored inside of a component using `this.state`. Storing data this way is useful when we're receiving that data from an external source or updating our component after a user has interacted with it (like incrementing a counter when a user clicks on it).

Sometimes we want to pass information from a parent component to child component in order to customize the way that child component renders. For this, we can use _props_ (short for _properties_).

Think about props as the options or configuration settings for a specific component. Props are one-time pieces of information that determine what the component should look like when it renders.

## An example of props: the donut bakery

Let's imagine we're building an application for a bakery. They want a way to highlight this week's featured donut on their website.

We might make a component that looks like this:

```jsx
class FeaturedDonut extends Component {
  render() {
    return (
      <h1>Today's featured Donut is: PB & J</h1>
    ) 
  }
}

class App extends Component {
  render() {
    return (
      <FeaturedDonut />
    ) 
  }
}
```

## Customizing our component with props

People LOVE this bakery's featured donuts. The bakery does a brisk trade in featured donuts. Featured donuts are their bread and butter, you could say. As such, they want the landing page of their website to show **three different** featured donuts.

We could modify the JSX inside our `FeaturedDonut` component to include the other two featured donuts, but what happens if elsewhere on the site they only want to feature one donut, not three, or a completely different set of donuts?

Let's create the ability to customize our `FeaturedDonut` component to display any flavor of donut we want depending on what options (a.k.a. props) we provide to it!

```jsx
class App extends Component {
  render() {
    return (
      <div>
        <FeaturedDonut name={"PB & J"} />
        <FeaturedDonut name={"Chocolate Glaze"} />
        <FeaturedDonut name={"Smore"} />
      </div>
    );
  }
}
```

Any attribute value that we give to our `FeaturedDonut` component will become accessible within the `FeaturedDonut` component through `this.props`.

This means that we can change our `FeaturedDonut` component to look like this:

```jsx
class FeaturedDonut extends Component {
  render() {
    return (
      <h1>Today's featured donut is: {this.props.name}</h1>
    )
  }
}
```

Now let's imagine that our awesome donut shop had some kind of database they were constantly updating with new featured donuts. Let's also pretend we've already grabbed this information and it's stored in our state like so:

```jsx
class FeaturedDonut extends Component {
  render() {
    return (
      <h1>Today's featured donut is: {this.props.name}</h1>;
    ) 
  }
}

class App extends Component {
  constructor() {
    super();
    this.state = {
      featuredDonuts: ["PB&J", "Apple Cinnamon", "Double Chocolate"]
    };
  }

  render() {
    return (
      <FeaturedDonut name="PB & J" />
    ) 
  }
}
```

We can use `map` to loop through `this.state.featuredDonuts` and feed the name of each individual donut to our `FeaturedDonut` component as a prop. Then, we can return all the featured donuts to the page like this:

```jsx
class App extends Component {
  constructor() {
    super();
    this.state = {
      featuredDonuts: ["PB & J", "Apple Cinnamon", "Double Chocolate"]
    };
  }

  render() {
    return (
      <div>
        {this.state.featuredDonuts.map(flavour => {
          return <FeaturedDonut name={flavour} />;
        })}
      </div>
    );
  }
}
```

This way, in the future, if more featured donuts get added to the state (i.e. the bakery's featured donut database), our `App` component will automatically render them all to the page!

**PRO TIP:** If you're ever unsure what's going to be in `this.props`, just `console.log` it out in your render function! (You can also find it in your React dev tools!)

## Passing functions as props

Let's create a new function within our `<App />` and name it `removeDonut`. We will use it to clear our featuredDonuts state. We will attach this function to a button element inside the`<FeaturedDonut />` component. To gain access to the function inside `<FeaturedDonut /> component, we need to pass a reference to it as a prop:

```jsx
  removeDonut = () => {
    this.setState({
      featuredDonuts: []
    })
  };

  render() {
    return (
      <div>
        {this.state.featuredDonuts.map(flavour => {
          return <FeaturedDonut removeDonut={this.removeDonut} name={flavour} />;
        })}
      </div>
    );
  }
}
```

```jsx
class FeaturedDonut extends Component {
  render() {
    return (
      <div>
        <h1>Today's featured donut is: {this.props.name}</h1>
        <button onClick={this.props.removeDonut}>Remove Donut</button>
      </div>
    );
  }
}
```

### Passing functions with parameters

Our `<FeaturedDonut />` component is successfully updating state in the parent `<App />` component. However, we are clearing all of our state on any button click. We only want the donut we click on to be removed. Since we are mapping through our state of featured donuts, we can pass the index value as a parameter to our `removeDonut` function. This will force us to change how we pass `removeDonut` as a prop:

```jsx
class App extends Component {
  constructor() {
    super();
    this.state = {
      featuredDonuts: ["PB & J", "Apple Cinnamon", "Double Chocolate"]
    };
  }

  removeDonut = index => {
    const oldDonuts = [...this.state.featuredDonuts];
    const updatedFeaturedDonuts = oldDonuts.filter((item, i) => i !== index);
    this.setState({
      featuredDonuts: updatedFeaturedDonuts
    });
  };

  render() {
    return (
      <div className="App">
        {this.state.featuredDonuts.map((flavour, index) => {
          return (
            <FeaturedDonut
              removeDonut={() => this.removeDonut(index)}
              name={flavour}
            />
          );
        })}
      </div>
    );
  }
}
```

A few significant changes took place here so let's break them down:

- We pass an arrow function inline with our custom function `removeDonut` as the return value. This way, we can include the index as an argument.
- In `removeDonut` we are making a copy of our state array using the spread operator and storing it in a new variable because we need to treat React state as immutable. 
- We filter through the copied array and return only the array item that matches our condition.
- `filter()` returns a new array and we can update our state with that new array from our `filter` function.
## Props and destructuring

So far our components have been fairly lightweight with only a few props. This won't always be the case and when it's not, we can take advantage of object destructuring to help improve our component readability. Let's imagine that our props object looks like the following:

```javascript
props = {
  author: {
    name: "Margaret Atwood",
    location: {
      city: "Toronto",
      province: "Ontario"
    }
  },
  review: "",
  date: "January 14, 1988"
};
```

```jsx
const authorDetails = props => {
  return (
    <div>
      <h1>{props.author.name}</h1>
      <h2>{props.author.location.city}</h2>
      <p>{props.review}</p>
    </div>
  );
};
```

With destructuring, we can remove the need to specify the props keyword:

```jsx
const AuthorDetails = ({ author, review }) => {
  return (
    <div>
      <h1>{author.name}</h1>
      <h2>{author.location.city}</h2>
      <p>{review}</p>
    </div>
  );
};
```

Destructuring works similarly in complex components, the main difference is that we will destructure our props within the `render()` method:

```jsx
class AuthorDetails extends Component {
  render() {
    const { author, review } = this.props;
    return (
      <div>
        <h1>{author.name}</h1>
        <h2>{author.location.city}</h2>
        <p>{review}</p>
      </div>
    );
  }
}
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

As apps grow in scale, it is valuable to start thinking about how we can better improve the quality of our code to help prevent bugs. One way we can achieve this is to validate the types of data (e.g. strings, numbers, etc) that we pass to our components through props. If the datatype that is passed through props is not what the component expects, a warning will be thrown to the console.

We can use the Proptypes library to do this kind of typechecking in React. To use it, we need to install it as a dependency in our app:

```javascript
npm install --save prop-types
```

After importing the Proptypes library, we can declare the expected datatypes for all the props in our component. Conventionally, this is written at the bottom of the component file, outside of its declaration:

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
- [Props vs. State](https://github.com/uberVU/react-guide/blob/master/props-vs-state.md) by the team at UberVU
