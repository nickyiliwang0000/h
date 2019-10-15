<!-- Student takeaway: -->
<!--Student will be able to:
- Differentiate between simple and complex components (e.g state + lifecycle methods)
- Understand that props help change how a simple component looks
-->

# Function components

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

For these situations we can reach for a _Function (Stateless) component_. Function components **do not** have state or access to the React lifecycle methods. (You may also see them called _presentational components_.) 

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

Does this look like something you've seen before? They are just **functions**! You can include them in your code just like class components:

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

Because presentational components cannot hold any state, you can provide information to them using **props**. 

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

In our [props lesson](https://github.com/HackerYou/bootcamp-notes/blob/master/react-and-firebase/props.md), we showed how to destructure props in a class component. You can also destructure props in a function component.

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

### Children Props 

You can use something called _children props_ or `props.children` to act as a container around some JSX you will be rendering when you invoke a component. This represents a kind of "slot" for furture content to be passed in. 

Here's an example of setting up children props in a function component:

```jsx
const Header = (props) => {
  return (
    <header>
      {props.children}
    </header>
  );
};
```
Here we're saying that whatever gets passed between the opening and closing `Header` tags will be rendered as children props. You could pass in one or many elements, or even other custom components, as long as they are imported and available in the file where this component is rendered.

Here's what this will look like where the example `Header` component is rendered:

```jsx
// inside rendering component 

<Header>
  <Logo />
  <h1>This is the title text</h1>
  <h2>This is a subtitle</h2>
</Header>
```
In this example we have 3 elements being passed in and rendered in the place where the children props were set up in our `Header` component. One custom component `Logo` and 2 native HTML elements `h1` and `h2`. It's important to remember that using children props requires a closing tag (rather than self-closing) becuase you need to sandwhich the children content between the two tags.

You can use children props in class components as well. Note that you would need the `this` keyword for setting up props: `this.props.children`.

To read more about children props, check out the [containment section](https://reactjs.org/docs/composition-vs-inheritance.html) of the react docs. 

## Code-along
We're going to refactor our art app to include function component(s).

<!-- Check the Trello card for a link to this code-along -->
<!-- finished code-along: https://hychalknotes.s3.amazonaws.com/dutch-art-react.zip -->

## Resources
* [Destructuring basics](https://medium.freecodecamp.org/the-basics-of-destructuring-props-in-react-a196696f5477)