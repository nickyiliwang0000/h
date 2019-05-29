<!-- Student takeaway: -->
<!--Student will be able to:
- Differentiate between simple and complex components (e.g state + lifecycle methods)
- Understand that props help change how a simple component looks
-->

# Reusable components

So far, we've been building all of our components like this:

```jsx
class App extends Component {
  render() {
    return (
      <div>
        {/* some stuff */}
      </div>
    )
  }
}
```

This is what's known as a _complex_ or _stateful_ component. In our applications, we'll often have most of the information about our program in the app's state.

The applications that we will make will usually have one or two complex components that hold all the state, and a bunch of components that do presentational tasks like render the title and image of every movie we have in state. These presentational components don't need state, they don't need lifecycle methods - they only need to render the component and return some JSX. 

The opposite of a complex component is a _simple component_. Simple components **do not** have state or access to the React lifecycle methods. (You may also see them called _stateless components_ or _presentational components_.) 

## Simple components

A simple component looks like this:

```javascript
const MySimpleComponent = () => {
  return (
    <div>
      <p>Hello friends!</p>
    </div>
  )
} 
```

You can include them in your code just like the more complex components:

```javascript
const MySimpleComponent = () => {
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
      <MySimpleComponent />
    </div>
    )
  }
}
```

Because simple components cannot hold any state, you can provide information to your simple components using **props**. 

As we learned in a previous lesson, props are a way to pass data from one component to another. Props are references to information that get passed between components and that affect the way components are rendered.

If we wanted to build a simple component that displayed a featured park, it might look like this:

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

### Destructuring simple components

In our [state v. props lesson](https://github.com/HackerYou/bootcamp-notes/blob/master/react-and-firebase/state-vs.-props.md), we showed how to destructure props in a complex component. You can also destructure props in a simple component.

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

Our simple component would look like this, initially:
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
We're going to refactor our art app to include simple component(s).

<!-- Check the Trello card for a link to this code-along -->
<!-- finished code-along: https://hychalknotes.s3.amazonaws.com/dutch-art-react.zip -->

## Resources
* [Destructuring basics](https://medium.freecodecamp.org/the-basics-of-destructuring-props-in-react-a196696f5477)