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

These components can be very complex because we can access multiple lifecycles methods, create functions, and define how we will manage our app state.

The applications that we will make will usually have a handful of complex components that hold all the state, and a bunch of components that do presentational tasks (ex. render the title and image of every movie we have in state in a parent component). These _presentational components_ don't need state or lifecycle methods - they only need to render the component and return some JSX. For these situations we can reach for a _function component_.

Note that until recently, class components were also known as _stateful_ components, and function components did not have state or access to the lifecycle methods. With the advent of React Hooks this is no longer the case; we will look at Hooks later in this course.


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

Does this look like something you've seen before? Function components are just **functions**! You can include them in your code just like class components:

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

Purely presentational components don't generally have any state. Instead, you provide information to them using props. 

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
Here, the `name` prop is being passed to the `FeaturedPark` component, where it will be rendered in our browser anywhere in `FeaturedPark`'s `render` method that it is referenced with `{props.name}`.


### Destructuring function components

In our [props lesson](https://github.com/HackerYou/bootcamp-notes/blob/master/react-and-firebase/props.md#props-and-destructuring), we showed how to destructure props in a class component. You can also destructure props in a function component.

Give a props object that looks like this:
```jsx
class App extends Component {
  constructor() {
    super();
    this.state = {
      author: {
        name: "Margaret Atwood",
        location: {
          city: "Toronto",
          province: "Ontario"
        }
      },
      review: "Really good at writing books.",
      date: "January 14, 1988"
    }
  }

  render() {
    return (
      <div>
        <AuthorDetails
          author={this.state.author}
          review={this.state.review}
          date={this.state.date}
        />
      </div>
    )
  }
}


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

To clean it up a bit though, we can destructure right in the argument:

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


### Children props 

Sometimes you may want a parent component to be able to variably render children - that is to say, you want a component that will act as a container that can have different child components or JSX in it. You can do this with _children props_, which you can think of like a "slot" for content to be passed into.

We pass components and/or JSX as children props by wrapping the content inside the tags of the parent element which will render it. This means that instead of being self-closing, our rendering component has both opening and closing tags:

```jsx
<Header>
  <Logo />
  <h1>Welcome to My Website</h1>
</Header>
```

Note above that the `Header` component is no longer self closing, because we are passing it another component (`Logo`) and a JSX element (`h1`) as children.

To render this content on the page, we have to call it inside our `Header` component. It is available to us as a property on the props object, `props.children`, which we can reference in our JSX:

```jsx
const Header = (props) => {
  return (
    <header>
      {props.children}
      <p>Some details about the website which will appear on all pages</p>
    </header>
  );
};
```

The above will result in a header which contains, in order, the contents of the `Logo` component, the `h1`, and then the `p`.

If on another page, we wanted a smaller header with no logo, a different `h1` and an `h2` tagline, we could call the `Header` component like this:

```jsx
<Header>
  <h1>The Blog</h1>
  <h2>Less Depressing but More Boring than Real News!</h2>
</Header>
```

This instance of the `Header` component will render a header with the blog `h1`, the `h2` tagline and, again, the `p`, since that is hard-coded into the `Header` component.

Whatever gets passed between the opening and closing of a component can be rendered as children props. You can pass in one or many elements, or other custom components, as long as they are imported and available in the file where they are being invoked.

You can use children props in class components as well, as `this.props.children`.

To read more about children props, check out the [containment section](https://reactjs.org/docs/composition-vs-inheritance.html) of the React docs. 


## Code-along
We're going to refactor our art app to include function component(s).

<!-- Check the Trello card for a link to this code-along -->
<!-- finished code-along: https://hychalknotes.s3.amazonaws.com/dutch-art-react.zip -->


## Resources
* [Destructuring basics](https://medium.freecodecamp.org/the-basics-of-destructuring-props-in-react-a196696f5477)