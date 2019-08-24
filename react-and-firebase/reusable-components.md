<!-- Student takeaway: -->
<!--Student will be able to:
- Differentiate between simple and complex components (e.g state + lifecycle methods)
- Understand that props help change how a simple component looks
-->

# Reusable components

So far, we've been building all of our components as Class Components, which look like this:

```jsx
class App extends Component {
  constructor(){
    super();
    this.state = {
      data: [],
    }
  }
  render() {
    return (
      <div>
        {/* some stuff */}
      </div>
    )
  }
}
```

These components can be very complex because we can access multiple lifecycles methods, create functions, and define how we will manage our app state. This method of creating components in React is what's known as a _stateful_ component. 

The applications that we will make will usually have a handful of stateful components that hold all the state, and a bunch of components that do presentational tasks like render the title and image of every movie we have in state. These presentational components don't need state, they don't need lifecycle methods - they only need to render the component and return some JSX. 

The opposite of a stateful component is a _Function (Stateless) component_. Function components **do not** have state or access to the React lifecycle methods. (You may also see them called _presentational components_.) 

## Function components

A function component looks like this:

```javascript
const MyFunctionComponent = () => {
  return (
    <div>
      <p>Hello friends!</p>
    </div>
  )
} 
```

You can include them in your code just like class components:

```javascript
const MyFunctionComponent = () => {
  return (
    <div>
      <p>Hello friends!</p>
    </div>
  )
} 

class App extends Component {
  render(){
    return (
    <div>
      <MyFunctionComponent />
    </div>
    )
  }
}
```

Because simple components cannot hold any state, you can provide information to your simple components using **props**. 

As we learned in a previous lesson, props are a way to pass data from one component to another. Props are references to information that get passed between components and that affect the way components are rendered.

If we wanted to build a function component that displayed a featured park, it might look like this:

```javascript
const FeaturedPark = (props) => {
  return (
    <div>
      <p>This week's featured park is: {props.name}.</p>
    </div>
  )
}

class App extends Component {
  render {
    return (
    <div>
      <FeaturedPark name="Riverdale" />
    </div>
    )
  }
}
```
Here, the `name` prop is being passed to the `FeaturedPark` component and should render in our browser wherever the code has `{props.name}`.

### Destructuring function components

In our [state v. props lesson](https://github.com/HackerYou/bootcamp-notes/blob/master/react-and-firebase/state-vs.-props.md), we showed how to destructure props in a class component. You can also destructure props in a function component.

Give a props object that looks like this:
```jsx
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

Our function component would look like this, initially:
```jsx
const AuthorDetails = props => {
  return (
    <div>
      <h1>{props.author.name}</h1>
      <h2>{props.author.location.city}</h2>
      <p>{props.review}</p>
    </div>
  );
};
```

We can destructure right in the argument:
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


## Code-along
We're going to refactor our art app to include function component(s).

<!-- Check the Trello card for a link to this code-along -->
<!-- finished code-along: https://hychalknotes.s3.amazonaws.com/dutch-art-react.zip -->

## Resources
* [Destructuring basics](https://medium.freecodecamp.org/the-basics-of-destructuring-props-in-react-a196696f5477)