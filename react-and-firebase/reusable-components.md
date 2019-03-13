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

But did you know that there's another way to create components? 

## Simple components
When you create a new React component using `class ____ extends _____`, you gain access to a lot of goodies: the ability to add state, lifecycle methods, etc. We will now refer to these components as _complex_ or _stateful_ components.

A lot of the time you'll be building a component that only needs to display a little bit of the user interface: it doesn't **need** to have state or lifecycle methods because all it's doing is rendering some information. We will call components like this _simple components_. (You may also see them called _stateless components_ or _presentational components_.) 

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

**Simple components cannot hold any state**. If you need to provide information to your simple components, you can do that using **props**. 

As we learned in a previous lesson, props are a way to pass data from one component to another. Props are information that gets passed from parent to child component which will affect the way the child component is rendered.

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

> You can destructure your props: check out [this article](https://medium.freecodecamp.org/the-basics-of-destructuring-props-in-react-a196696f5477) or search around for some blog posts on how to do that.

## Code-along
We're going to refactor our art app to include simple component(s).

<!-- Check the Trello card for a link to this code-along -->
<!-- finished code-along: https://hychalknotes.s3.amazonaws.com/dutch-art-react.zip -->