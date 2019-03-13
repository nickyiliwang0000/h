<!-- Student takeaway: -->
<!--Student will be able to:
- Differentiate between simple and complex components (e.g state + lifecycle methods)
- Understand that props help change how a simple component looks
-->

# Reusable components

So far, we've been building all of our components like this:

```javascript
class App extends Component {
  render() {
    return (
      <div>
        My application!
      </div>
    )
  }
}
```

This is what's known as a _complex_ or _stateful_ component. In our applications, we'll often have most of the information about our program in the App's state.

The applications that we will make will usually have one or two complex components that hold all the state, and a bunch of components that do presentational tasks like render the title and image of every movie we have in state. These presentational components don't need state, they don't need lifecycle methods - they only need to render the component and return some JSX. 

The opposite of a complex component is a _simple component_. Simple components **do not** have state or access to the React lifecycle methods. (You may also see them called _stateless components_ or _presentational components_.) 

## Simple components

A simple component looks like this:

```javascript
const MySimpleComponent = () => {
  return (
    <div>
      Hello friends!
    </div>
  )
} 
```

You can include them in your code just like the more complex components:

```javascript
const MySimpleComponent = () => {
  return (
    <div>
      Hello friends!
    </div>
  )
} 

class App extends Component {
  return (
  <div>
    <MySimpleComponent />
  </div>
  )
}
```

Because simple components cannot hold any state, you can provide information to your simple components using **props**. 

As we learned in a previous lesson, props are a way to pass data from one component to another. Props are references to information that get passed between components and that affect the way components are rendered.

If we wanted to build a simple component that displayed a featured donut, it might look like this:

```javascript
const FeaturedDonut = (props) => {
  return (
    <div>
    <p>Our featured donut is {props.name}.</p>
    </div>
  )
}

class App extends Component {
  render {
    return (
    <div>
      <FeaturedDonut name="PB&J" />
    </div>
    )
  }
}
```
Here, the `name` prop is being passed to the `FeaturedDonut` component and should render in our browser wherever the code has `{props.name}`.

> You can destructure your props: check out the [state v. props lesson](https://github.com/HackerYou/bootcamp-notes/blob/master/react-and-firebase/state-vs.-props.md) or [this article](https://medium.freecodecamp.org/the-basics-of-destructuring-props-in-react-a196696f5477) or search around for some blog posts on how to do that.

## Code-along
We're going to refactor our art app to include simple component(s).

<!-- Check the Trello card for a link to this code-along -->
<!-- finished code-along: https://hychalknotes.s3.amazonaws.com/dutch-art-react.zip -->