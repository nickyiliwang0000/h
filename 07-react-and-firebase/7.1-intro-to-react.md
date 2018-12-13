<!-- Student takeaway: -->
<!--Student will be able to:
- Understand when to use React
- Install React dev tools 
- Create a new React app using create-react-app in the command line
- Know what goes in index.js and what goes in App.js
- Understand what a component is
- Understand how to nest a component
- Understand that components are self-closing
- Know a few common JSX gotchas
 -->

# Intro to React

_React.js_ is a JavaScript library created by Facebook for building user interfaces and single page applications. React is especially good at taking in user input and quickly changing the user's interface to reflect that input. What React does that the traditional HTML/CSS/JS model doesn't is it only updates the part of the DOM that **needs** updating (e.g. the number of items in a shopping cart) rather than reloading the whole page from scratch.

For this reason, React is the library of choice for apps like [Facebook](http://www.facebook.com/), [Instagram](http://www.instagram.com) and [AirBnB](http://www.airbnb.com/), that have lots of moving parts. 

Websites built totally in React are _single page applications_. An SPA is a kind of website that loads a single HTML file and uses AJAX to update the DOM without reloading the page. You've already built some SPAs: your API projects, for example!


## Installing the React developer tools
Before we start writing any code, let's install the React developer tools. This is an extension for your browser that will let us inspect our React applications alongside our normal developer tools.

[Click here to download the React Developer Tools for Chrome.](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en)

[Click here to download the React Developer Tools for Firefox.](https://addons.mozilla.org/en-US/firefox/addon/react-devtools/)

Let's inspect those sites we were looking at before and see what we find!

## Create React App
To build React projects, we will be using a tool built by React's developers called _Create React App_.

### Installing Create React App
We're going to install Create React App via the _node package manager_(npm) using the command line.

```bash
npm i -g create-react-app
```

With `create-react-app` installed, we are able to quick start applications with the `create-react-app` command. Typing `create-react-app my-first-app` into your command line will create a folder called `my-first-app` and inside will be all the boilerplate needed to start building a React app! It will also give you instructions on how to run your application.

### Build your first app with Create React App
The Create React App tool gives us everything we need to get started and it's important to know what some of the files do. In the project folder you will find a `src` folder, which will contain a bunch of files that Create React App made just for you! Let's look at a few of the important ones: `index.js` and `App.js`.

#### `index.js`

The `index.js` file contains all the information needed to render our React application to the page. 

```javascript
//index.js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import registerServiceWorker from './registerServiceWorker';

ReactDOM.render(<App />, document.getElementById('root'));
registerServiceWorker();
```

Notice that we import `React` and `ReactDom` in this file. `react-dom` [is a module](https://github.com/HackerYou/bootcamp-notes/blob/master/06-applied-javacript/6.17-making-our-code-more-modular.md#what-are-modules) needed to render our application to the DOM. (There is a version of React that can be used server-side as well.)

After that, we import `index.css`. With the Create React App system, we import our CSS straight into the JavaScript. This allows the underlying system that runs Create React App to bundle up the JavaScript and CSS in the most effective way.

The `App` component is also imported and rendered to the page using `ReactDOM.render()`. This `App` component is the place where we will be writing most of our code.

Don't worry about `registerServiceWorker` - just know that you need it for now. [Keeners can click here.](https://stackoverflow.com/questions/47953732/what-does-registerserviceworker-do-in-react-js)

#### `App.js`

This file is the main component of our application and the file you'll be spending most of your time in.

```javascript
//App.js
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';

class App extends Component {
  render() {
    return (
      <div className="App">
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <h1 className="App-title">Welcome to React</h1>
        </header>
        <p className="App-intro">
          To get started, edit <code>src/App.js</code> and save to reload.
        </p>
      </div>
    );
  }
}

export default App;

```

This file has three lines of imports: 
 * a couple of functions from `react` (don't worry too much about this right now)
 * an image from `./logo.svg` 
 * CSS for the `App` component

The `App` component is a `class` that extends the `Component` class from React. This class has a `render` method, and inside the render method we define the HTML we want to show on the page. But what looks like HTML there... is actually not HTML! Weird, right? It's something called _JSX_ (JavaScript XML) and we'll talk about it more at the end of this lesson.

Enough talk! Let's get this app running and create our first component. In order to start everything, we need to use the `npm start` command on our command line. Make sure you are **inside** the folder Create React App made for you, then run `npm start`.

### What is a component?

A _component_ is a small reusable chunk of code that is usually responsible for rendering one piece of UI. A React application can contain hundreds of components that render each other and interact with each other thus composing the UI of your application. 

Let's make some of our own components. Start by creating a new file called `Header.js` in the `src` folder. 

Inside `Header.js`, write the following:
```javascript
// Header.js
import React from 'react';

class Header extends React.Component {
  render() {
    return (
      <header>
        <h1>My header!!</h1>
      </header>
    )
  }
}

export default Header;
```

Go back to `App.js` and import our new component like this:

```javascript
import Header from './Header';
```

We can now use the `<Header />` component in the `App.js` file. 

```javascript
//App.js
class App extends Component {
  render() {
    return (
      <div className="App">
        <Header />
        <p className="App-intro">
          To get started, edit <code>src/App.js</code> and save to reload.
        </p>
      </div>
    );
  }
}
```

Try making a new component called `Footer` and add it to the bottom of the `div` with a class of `App`.

### JSX 

JavaScript XML (JSX) is a syntax extension for JavaScript that can be passed into React's `render` method and compiled into HTML elements. It looks a lot like HTML, but it has a few gotchas.

#### JSX gotchas

* Since it's basis is JavaScript, not HTML, we can't use certain HTML attributes in JSX because they are reserved words in JavaScript. 

  HTML | JSX
  ---|---
  `class`|  `className`  
  `for` | `htmlFor`

* JSX elements are treated as **JavaScript expressions**, so they can be used as variables, passed to functions, or stored in objects or arrays. 
  * Remember that an **expression** is anything that produces a value. For example, `2 + 2` is an expression because it returns `4`.


* Each JSX element must return **only one** HTML element (we'll be using `<div>` for most of the class)

* In order to render your elements to the screen, you **must use** the `ReactDOM` library (specifically, it's `render` method).

* One other gotcha is what JavaScript you can put inside of JSX. Anything that is inside of `{}` after the return must be an expression. This gets challenging when you only want to render a piece of your UI )_sometimes_. 

  * You will be tempted to put an `if` statement in your JSX like this: 
    ```javascript
    render() {
      return (
        <div>
          {if(userIsLoggedIn) {
            <h1>Welcome, friend!</h1>
          }}
        </div>
      )
    }
    ```
    But `if` statements are _statements_, not expressions.

  * React has lots of ways to get around this. One is to use a ternary operator:
    ```javascript
    render() {
      return (
        <div>
        {userIsLoggedIn ? <h1>Welcome, friend!</h1> : null}
        </div>
      )
    }
    ```
    The code above is saying: if the variable `userIsLoggedIn` is `true`, return the `h1` tag, otherwise don't return anything. 

  * Using ternary operators to conditionally render content can get complicated pretty quickly, so it is also common to use functions or variables **outside** of the return to accomplish this:
    ```javascript
    render() {
      let markupShowingOnPage = null;

      if(userIsLoggedIn) {
        markupShowingOnPage = <h1>Welcome, friend!</h1> 
      }

      return (
        <div>
        {markupShowingOnPage}
        </div>
      )
    }
    ```

### Nesting and splitting components
One of the incredibly powerful features of React is the ability to organize and split your code into components and then arrange and rearrange them like Lego.

For example, let's say we wanted to create a search bar component for our application.

We'd create a new `SearchBar` component above your `App` component:
```javascript
//App.js
class SearchBar extends React.Component {
  render() {
    return (
      <input type="text" placeholder="Enter your search term" name="search" />
    )
  }
}
class App extends React.Component { 
  // All that App stuff
}
```

And then you can nest it within your `App` component like so:

```javascript
//App.js
class App extends React.Component {
  render() {
    return (
      <div className="App">
        <Header />
        <SearchBar />
        <p className="App-intro">
        To get started, edit <code>src/App.js</code> and save to reload.
        </p>
      </div>
    )
  }
}
```

Your `SearchBar` component should now appear inside your `App` component in the browser!

What's really great about mixing and matching components this way is that it allows for a ton of code re-use. If we want the same `SearchBar` to appear in ten different places on the website, we don't have to rewrite the code for it ten times - we just have to insert the `<SearchBar />` component anywhere we need it!

Also - you'll notice that when we write out the `<SearchBar />` component that we include a `/` at the end. This is because our React elements are always **self-closing elements**. Just like in HTML and JSX, any time we create a component that doesn't have any children, we let React know by adding a `/`.

#### Component kitchen - cook 'em up!
Practice making a few new components of your own choosing and nesting them inside your `<App>` component. They can do whatever you want - this is just to practice and get used to the class component syntax.

### Sass and Create React App
In order to use Sass when working with Create React App, we need to add a few things.  You can find a write up of this in [the documentation for Create React App](https://facebook.github.io/create-react-app/docs/adding-a-sass-stylesheet#docsNav). 

The React docs don't recommend it:

``` bash
Generally, we recommend that you don’t reuse 
the same CSS classes across different components. 
For example, instead of using a .Button CSS class 
in <AcceptButton> and <RejectButton> components, 
we recommend creating a <Button> component with 
its own .Button styles, that both <AcceptButton> 
and <RejectButton> can render (but not inherit).
```
First, install `node-sass`:

```bash
$ npm install node-sass --save
$ # or
$ yarn add node-sass
```
Then you should be able to import `.scss` files:

```bash
@import 'styles/_colors.scss'; // assuming a styles directory under src/
@import '~nprogress/nprogress'; // importing a css file from the nprogress node module
```

But you can do whatever you want!
<!-- 

To use Sass, we'll need to install two packages:
* `node-sass-chokidar` (to compile our Sass)
* `npm-run-all` (to run our development server)

```bash
npm install --save node-sass-chokidar npm-run-all
```
>_Chokidar_ is a Hindi-dervied English word that means `private watchperson` or `gate security person`. The Sass chokidar is watching your Sass files for changes! 

Now that both of those are installed, we need to change the `package.json` file to be able to use the,. Our `scripts` section should now look like this:

```json
  "scripts": {
    "build-css": "node-sass-chokidar src/ -o src/",
    "watch-css": "npm run build-css && node-sass-chokidar src/ -o src/ --watch --recursive",
    "start-js": "react-scripts start",
    "start": "npm-run-all -p watch-css start-js",
    "build-js": "react-scripts build",
    "build": "npm-run-all build-css build-js",
    "test": "react-scripts test --env=jsdom",
    "eject": "react-scripts eject"
  }
```
Now, when we use the `npm start` command, the `npm-run-all` package will set up our local server and watch our JS and our chokidar will watch our Sass files. -->

### Additional Resources
* [React for Beginners](https://reactforbeginners.com/) (taught by HackerYou instructor Wes Bos!)
* [Learning React: Getting Started and Concepts](https://scotch.io/tutorials/learning-react-getting-started-and-concepts)
* [Hello World in React](http://codepen.io/gaearon/pen/ZpvBNJ?editors=0010) (a CodePen you can play around with)