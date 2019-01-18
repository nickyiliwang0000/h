# What is routing?	
If you have wireless internet in your home, you might already be familiar with how a router works. In your home, your router directs the data between your devices and the internet: it's kind of like an air traffic controller for your data.

The same concept can be applied to our React applications. Right now, all of our apps have only had one page to speak of (we'll call this a _view_), but what happens if we want to show different views? React Router, a router package written by some people who wanted to solve this problem, can help direct our users between different views, prevent users from seeing things they shouldn't, and make sure that our application always delivers the correct view.

In essence, **React Router simulates the kind of behaviour we would see from a multi-page site (the ability to navigate between pages), but within the context of a single page application.**

## Building a personalweb site using React Router
In order to understand the basics of how React Router works, we're going to build a simple personal website with links to contact and about sections.

## Setting up React Router
Create a new React app using `create-react-app` and then install the `react-router-dom` package.

`npm install react-router-dom --save-dev`

Now that we've installed and configured `react-router`, let's set up our root `App` component.

`react-router-dom` is an npm module, so we can `import` it much in the same way that we import `react` and `react-dom`:

```javascript
import { 
	BrowserRouter as Router, 
	Route, Link } from 'react-router-dom';
```

You'll notice that our React Router import looks slightly different than our `React` and `ReactDOM` inputs. We have two curly brackets, followed by three comma separated names: `Router`, `Route`, and `Link`. 

Each of these is a `named export` (more on this in our lesson on ES6 modules). React Router has a lot of different internal functions and methods, but right now we only need `BrowserRouter`, `Route`, and `Link`, so we can just grab those three named functions. This can help simplify our application and also decreases load time. You will notice `Router` is a bit special: we have this phrase `BrowserRouter as Router`. This is how we rename something that is exported from a module in our file. The thing that is available for us to `import` is called `BrowserRouter` but we change it to `Router` it using the `as` keyword.

Now let's create a few components so we can add routing to our application:

```javascript
//App.js
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';
import {
  BrowserRouter as Router,
  Route,
  Link
} from 'react-router-dom'

class About extends Component {
	render() {
		return (
			<h2>
				About Us
			</h2>
		)
	}
}

class Contact extends Component {
  render() {
    return (
      <h2>
        Contact Us
			</h2>
    )
  }
}


class App extends React.Component {
  render() {
    return (
      <Router>
        <div>
          <h1>My Personal Webpage!</h1>
          <Route path="/about" component={About} />
          <Route path="/contact" component={Contact} />
        </div>
      </Router>
    )
  }
}

export default App;
```

Here we use our `App` component as the location for our router. The `App` component returns a `Router` component that wraps our HTML. (`Router` should only have one child, so wrap your content in a `div`or a `Fragment` if you need to.) Inside the `Router`, we can place `<Route />` components that will help us display specific content. When we go to a specified path that matches the `path` attribute of a  `<Route />`,  our application it will render that matched component!

## Adding links
Since React Router is now controlling how we navigate within our app, we can make use of its special `<Link >` component, which allows the user to navigate between views. To access this component, we need to import it with the other named exports from React Router at the top of our page:

```javascript
import React, { Component } from 'react'
import { 
	BrowserRouter as Router, 
	Route, Link } from 'react-router-dom';
```

And now we can use `<Link >` much the same way we use the `<a href="#" >` element:

```javascript
class App extends Component {
	render() {
		return (
			<Router>
				<div>
					<h1>My Personal Webpage!</h1>
					<Link to="/about">About</Link>
					<Link to="/contact">Contact</Link>
					<Route path="/about" component={About} />
					<Route path="/contact" component={Contact} />
				</div>
			</Router>
		)
	}
}
```

With this, we can navigate between our components! Pretty amazing. You'll notice that we can use the browser's back and forward buttons and stay within our app.

## Nesting routes
A great thing about React Router is that we can create nested routes. Let's say we want to render some contact information for a specific member of our organization. In order to make this happen we need to modify our `Contact` component and include a `<Route />` to that contact information.

```javascript
class Contact extends Component {
	render() {
		return (
			<div>
				<h2>Contact</h2>
				<Link to="/contact/michelle">Michelle</Link>
				<Route path="/contact/michelle" component={Michelle} />
			</div>
		);
	}
}

class Michelle extends Component {
	render() {
		return (
			<p>Email: <a href="mailto:michelle@destinyschild.com">michelle@destinyschild.com</a></p>
		);
	}
}
```

Now when we go to the contact page and click the `Michelle` link, we will see her info appear below her name!

### Bonus: Styling active links with React Router
By adding the `activeStyle` attribute to your `NavLink` component (which you've gotta import up at the top with `Link`) you can highlight whichever link is pointing to the current active route. Try adding the `activeStyle` attribute to your links like this:

```javascript
<NavLink to="/about" activeStyle={{ color: "red" }}>About</NavLink>
```
You can also add an active class name using the `activeClassName` attribute, like so:

```javascript
<NavLink to="/about" activeClassName="active">About</NavLink>
```

And then your CSS, you need to add a corresponding `.active` class. (The class does not need to be named `active` but the attribute in `NavLink` DOES need to be named `activeClassName`.)

```css
.active{
	background:orange;
}
```

## URL params
Sometimes it can be valuable to pass information from one route to another in order to provide some context as to how an upcoming view should be displayed. We can accomplish this using URL params.

Adding a route that accepts URL params isn't too complicated: we add `:paramName` to the end of our `<Route />` tag, like this:

`<Route path="/route/:param" component={ComponentName} />`

In your open file, change the route for the About page to include a `skill` parameter:

```javascript
//App.js
class App extends Component {
  render() {
    return (
      <Router>
        <div>
          <h1>My Personal Webpage!</h1>
          <NavLink activeStyle={{ color: 'red' }} to ="/about">About</NavLink>
          <NavLink activeClassName="active" to ="/contact">Contact</NavLink>
          <Route path="/about/:skill" component={About} />
          <Route path="/contact" component={Contact} />
        </div>
      </Router>
    )
  }
}
```

Then, use this parameter somewhere in your About component:

```javascript
class About extends Component {
  render() {
    return (
      <div>
        <h2>About Me</h2>
        <p>I am an expert at {this.props.match.params.skill}!</p>
      </div>
    )
  }
}
```
When you go to `localhost:3000/about/javascript`, you should see that you are en expert at JavaScript!

![browser rendering of phrase I am an expert at javascript](https://hychalknotes.s3.amazonaws.com/routing-params-example-.png)

Another example:
Let's say, for fun, we were building an apology generator that would generate a custom apology for a user based on their name:

```javascript
import React, { Component } from 'react'
import { 
	BrowserRouter as Router, 
	Route, Link } from 'react-router-dom';

class Apology extends Component {
	render(){
		return (
      <div>
			<h1>Dear {this.props.match.params.name},</h1>
			<p>I am so sorry that I watched the next episode of our show without consulting you. That was selfish of me.</p>
      </div>
		)
	}
}

class App extends Component {
	render() {
		return (
			<Router>
				<Route path="/apology/:name" component={Apology} />
			</Router>
		)
	}
}

export default App
```

Now try navigating to `localhost:3000/apology/anyname` and see that the content will be customized based on what name you put in! This is kind of a silly example, but hopefully it gets you thinking about how params work and how information can be shared between views.

## Codealong: Movie catalogue
Now that we have a rough understanding of how params work, let's build an app that can catalogue and display movies so that we better understand when and how to use params.

### Additional resources
* [React Router GitHub Repo](https://github.com/ReactTraining/react-router)
* [React Router params tutorial](https://github.com/reactjs/react-router-tutorial/tree/master/lessons/06-params)
* [Beginner's Guide to React Router](https://medium.com/@dabit3/beginner-s-guide-to-react-router-53094349669) is for an older version of React Router, but covers many important concepts related to using `react-router`.