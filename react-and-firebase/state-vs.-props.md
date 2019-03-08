# Props, and how they differ from state in React

In our previous lesson on state, we saw how information can be stored inside of a component using `this.state`. Storing data this way is useful when we're receiving that data from an external source or updating our component after a user has interacted with it (like incrementing a counter when a user clicks on it).

Sometimes we want to pass information from a parent component to child component in order to customize the way that child component renders. For this, we can use _props_ (short for _properties_).

Think about props as the options or configuration settings for a specific component. Props are one-time pieces of information that determine what the component should look like when it renders.

## An example of props: the donut bakery 
Let's imagine we're building an application for a bakery. They want a way to highlight this week's featured donut on their website. 

We might make a component that looks like this:

```javascript
class FeaturedDonut extends Component {
	render() {
		return (
			<h1>Today's featured Donut is: PB&J</h1>
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
People LOVE this bakery's featured donuts. The bakery does a brisk trade in featured donuts. Featured donuts are their bread and butter, you could say. As such, they want the front page to show **three different** featured donuts.

We could modify the JSX inside our `FeaturedDonut` component to include the other two featured donuts, but what happens if elsewhere on the site they only want to feature one donut, not three, or a completely different set of donuts?

Let's create the ability to customize our `FeaturedDonut` component to display any flavor of donut we want depending on what options (a.k.a. props) we provide to it!

```javascript
class App extends Component {
	render() {
		return (
			<div>
				<FeaturedDonut name={"PB&J"} />
				<FeaturedDonut name={"Chocolate Glaze"} />
				<FeaturedDonut name={"Smore"} />
			</div>
		)
	}
}
```

Any attribute value that we give to our `FeaturedDonut` component will become accessible within the `FeaturedDonut` component through `this.props`. 

This means that we can change our `FeaturedDonut` component to look like this:

```javascript
class FeaturedDonut extends Component {
	render() {
		return (
			<h1>Today's featured Donut is: {this.props.name}</h1>
		)
	}
}
```

Now let's imagine that our awesome donut shop had some kind of database they were constantly updating with new featured donuts. Let's also pretend we've already grabbed this information and it's stored in our state like so:

```javascript
class FeaturedDonut extends Component {
	render() {
		return (
			<h1>Today's featured Donut is: {this.props.name}</h1>
		)
	}
}

class App extends Component {
	constructor() {
		super()
		this.state = {
			featuredDonuts: ['PB&J', 'Apple Cinnamon', 'Double Chocolate']
		}
	}

	render() {
		return (
			<FeaturedDonut name='PB&J' />
		)
	}
}
```

We can use `map` to loop through `this.state.featuredDonuts` and feed the name of each individual donut to our `FeaturedDonut` component as a prop. Then, we can return all the featured donuts to the page like this:

```javascript
class App extends Component {
	constructor() {
		super()
		this.state = {
			featuredDonuts: ['PB&J', 'Apple Cinnamon', 'Double Chocolate']
		}
	}

	render() {
		return (
			<div>
				{this.state.featuredDonuts.map((donut) => {
 					return <FeaturedDonut name={donut} />
				})}
			</div>
		)
	}
}
```

This way, in the future, if more featured donuts get added to the state (i.e. the bakery's featured donut database), our `App` component will automatically render them all to the page!

**PRO TIP:** If you're ever unsure what's going to be in `this.props`, just `console.log` it out in your render function! (You can also find it in your React dev tools!)

## So what's the difference between state and props?
When you're first starting to build React applications and you need to handle data inside a component, it's often hard to tell whether you should be using props or state.

Here are a few guidelines that can help you determine which one you need to use:
* Props are always passed down from a parent component to its child: they help the child determine what it should look like
* A component **cannot** modify props that it has received. So if your component has some piece of data that you know is going to need to be updated over time, then it probably makes more sense for it to be state.
* If you're handling some kind of user interaction (like a click event, for example), chances are you'll store that information in state.

Some of you may find this rudimentary flowchart helpful:
![state and props flowchart](https://hychalknotes.s3.amazonaws.com/state-props-flowchart-2018.png)

### Additional Resources
* [React Docs on Props vs. State](https://facebook.github.io/react/docs/state-and-lifecycle.html)
* [Props vs. State](https://github.com/uberVU/react-guide/blob/master/props-vs-state.md) by the team at UberVU
