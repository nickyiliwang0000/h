# Complex and simple components

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

But did you know that there's a simpler way that you can create components? 

## Simple components
When you create a new React component using `class extends`, you gain access to a lot of goodies: the ability to add state, lifecycle hooks, etc. We will now refer to these components as _complex_ or _stateful_ components.

A lot of the time you'll be building a component that just needs to display a little bit of the user interface: it doesn't need to have state or lifecycle hooks because it's just rendering some information. We will call components like this _simple components_. (You may also see them called _stateless components_ or _presentational components_.) 

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

You can include them in your code just like the more complex `class extends`-style components:

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

As we learned in lesson 7.5, props are a way to pass data from one component to another. For this exercise, think of a prop as information that gets passed from parent to child component which will affect the way the child component is rendered.

For example, if we wanted to build a simple component that displayed a featured donut, it might look like this:

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

## Code-along
We're going to refactor our art app to include simple component(s).
