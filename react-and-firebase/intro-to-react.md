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

### Installing with Create React App
We're going to use Create React App via the _node package manager_ (npm/npx) on the command line to make our first app.

```bash
npx create-react-app my-first-app
```

Typing `npx create-react-app my-first-app` into your command line will create a folder called `my-first-app` and inside will be all the boilerplate needed to start building a React app! It will also give you instructions on how to run your application.

### Build your first app with Create React App
The Create React App tool gives us everything we need to get started and it's important to know what some of the files do. In the project folder you will find a `src` folder, which will contain a bunch of files that Create React App made just for you! Let's look at a few of the important ones: `index.js` and `App.js`.

#### `index.js`
The `index.js` file contains all the information needed to render our React application to the page. You won't need to make any edits to this file.

```jsx
//index.js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import registerServiceWorker from './registerServiceWorker';

ReactDOM.render(<App />, document.getElementById('root'));
registerServiceWorker();
```

Notice that we import `React` and `ReactDOM` in this file. `react-dom` [is a module](https://github.com/HackerYou/bootcamp-notes/blob/master/06-applied-javacript/6.17-making-our-code-more-modular.md#what-are-modules) needed to render our application to the DOM. (There is a version of React that can be used server-side, called _Next.js_, which doesn't need this file.)

After that, we import `index.css`. With the Create React App system, we import our CSS straight into the JavaScript. This allows the underlying system that runs Create React App to bundle up the JavaScript and CSS in the most efficient way.

The `App` component is also imported and rendered to the page using `ReactDOM.render()`. This `App` component is the place where we will be writing most of our code.

Don't worry about `registerServiceWorker` - just know that you need it for now. [Those interested can click here.](https://stackoverflow.com/questions/47953732/what-does-registerserviceworker-do-in-react-js)

#### `App.js`

This file is the main component of our application and the file you'll be spending most of your time in.

```jsx
//App.js

// a couple of functions from the React library
import React, { Component } from 'react';

// an image from `./logo.svg` 
import logo from './logo.svg';

// CSS for the `App` component
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}

export default App;
```
As you can see, `App()` is a function. We're going to refactor this function to be a class, like this:

```js
//App.js

// a couple of functions from the React library
import React, { Component } from 'react';

// an image from `./logo.svg` 
import logo from './logo.svg';

// CSS for the `App` component
import './App.css';

class App extends Component{
  render(){
      return (
        <div className="App">
          <header className="App-header">
            <img src={logo} className="App-logo" alt="logo" />
            <p>
              Edit <code>src/App.js</code> and save to reload.
            </p>
            <a
              className="App-link"
              href="https://reactjs.org"
              target="_blank"
              rel="noopener noreferrer"
            >
              Learn React
            </a>
          </header>
        </div>
      );
  }
}

export default App;
```

Here, `App` is a class that extends the `Component` class from React, which has a `render` method. Inside the `render` method we define the HTML we want to show on the page. But what looks like HTML there... is actually not HTML! Weird, right? It's something called _JSX_ (JavaScript XML) and we'll talk about it more at the end of this lesson.

Enough talk! Let's get this app running and create our first component. In order to start everything, we need to use the `npm start` command on our command line. Make sure you are **inside** the folder Create React App made for you, then run `npm start`.

### What is a component?

A _component_ is a small reusable chunk of code that is usually responsible for rendering **one** piece of the user interface. A React application can contain hundreds of components that render each other and interact with each other thus composing the UI of your application. 

Let's make some of our own components. Start by creating a new file called `Header.js` in the `src` folder. 

Inside `Header.js`, write the following:
```jsx
// Header.js
import React, { Component } from 'react';

class Header extends Component {
  render() {
    return (
      <header>
        <h1>Welcome to the Toronto Parks' website</h1>
      </header>
    )
  }
}

export default Header;
```

Go back to `App.js` and import our new component like this:

```javascript
//App.js
import Header from './Header.js';
```

We can now use the `<Header />` component in the `App.js` file. 

```jsx
//App.js
class App extends Component {
  render() {
    return (
      <div className="App">
        <Header />
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <p>
            Edit <code>src/App.js</code> and save to reload.
          </p>
          <a
            className="App-link"
            href="https://reactjs.org"
            target="_blank"
            rel="noopener noreferrer"
          >
            Learn React
          </a>
        </header>
      </div>
    );
  }
}
```
Let's get that default header element out of there:

```js
//App.js
class App extends Component {
  render() {
    return (
      <div className="App">
        <Header />
      </div>
    );
  }
}

```

Try making a new component called `Footer` and add it inside `div.App`.

### JSX 

JavaScript XML is a syntax extension for JavaScript that can be passed into React's `render` method and compiled into HTML elements. It looks a lot like HTML, but it has a few gotchas.

#### JSX gotchas

* Since its basis is JavaScript, not HTML, we can't use certain HTML attributes in JSX because they are reserved words in JavaScript. 

  HTML | JSX
  ---|---
  `class`|  `className`  
  `for` | `htmlFor`

* JSX elements are treated as **JavaScript expressions**, so they can be used as variables, passed to functions, or stored in objects or arrays. 
  * Remember that an **expression** is anything that produces a value. For example, `2 + 2` is an expression because it returns `4`.


* Each JSX element must return **only one** HTML element (we'll be using `<div>` for most of the class, but you may see `<Fragment>` in the wild).

* In order to render your elements to the screen, you **must use** the `ReactDOM` library (specifically, its `render` method).

* One other gotcha is what JavaScript you can put inside of JSX. Anything that is inside of `{}` after the return must be an expression. This gets challenging when you only want to render a piece of your UI  _conditionally_. 

  * You will be tempted to put an `if` statement in your JSX like this: 
    ```jsx
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
    But `if` statements are **statements**, not expressions.

  * React has lots of ways to get around this. One is to use a ternary operator:
    ```jsx
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
    ```jsx
    render() {
      let markupShowingOnPage = null;

      if(userIsLoggedIn) {
        markupShowingOnPage = `<h1>Welcome, friend!</h1>`;
      }

      return (
        <div>
          {markupShowingOnPage}
        </div>
      )
    }
    ```
* VSCode's Emmet will not work in  JSX unless you enable it in your user settings. To enable it go [follow these directions](https://medium.com/@eshwaren/enable-emmet-support-for-jsx-in-visual-studio-code-react-f1f5dfe8809c).

### Fragments

We've already seen that JSX elements can only return one HTML element or component. If we try to return multiple, we will get a warning saying “JSX parent expressions must have one parent element." 

 ```jsx
return(
    <p>I'm a paragraph!</p>
    <p>I'm a second paragraph!</p>
)
```
 The easiest way to handle this is by wrapping the elements in a `<div>` :

  ```jsx
return(
    <div>
        <p>I'm a paragraph!</p>
        <p>I'm a second paragraph!</p>
    </div>
)
```

The downside is we ends up rendering a lot of extra `divs` to our page that we don't need, causing issues with accessibility and even layouts.

We can work around this by using a **fragment**. Fragments let you group a list of children without adding extra nodes to the DOM [(from the ReactJS docs)](https://reactjs.org/docs/fragments.html). This keeps us from ending up with too many extra `divs`!

To use a fragment, place the list of children inside `<React.Fragment> </React.Fragment>` or the shorthand: `<> </>` (that's not a typo, it really is two angle brackets with nothing inside!). 

  ```jsx
return(
    <React.Fragment>
        <p>I'm a paragraph!</p>
        <p>I'm a second paragraph!</p>
    </React.Fragment>
)
```
While the shorthand will save us time, if we want to use the `key` attribute, we need to use the explicit `<React.Fragment>` syntax. As well, `key` is currently the only attribute that can be passed to fragments.

### Nesting and splitting components
One of the incredibly powerful features of React is the ability to organize and split your code into components and then arrange and rearrange them like Lego.

For example, let's say we wanted to create a search bar component for our application.

We'd create a new `SearchBar.js` file:
```jsx
//SearchBar.js

class SearchBar extends Component {
  render() {
    return (
      <input type="text" placeholder="Enter your search term" name="search" />
    )
  }
}
```

And then you can nest it within your `Header` component like so:

```jsx
// Header.js
import React, { Component } from 'react';
import SearchBar from './SearchBar';

class Header extends Component {
  render() {
    return (
      <header>
        <h1>Welcome to the Toronto Parks' website</h1>
        <SearchBar />
      </header>
    )
  }
}

export default Header;
```

Your `SearchBar` component should now appear inside your `Header` component in your app!

What's really great about mixing and matching components this way is that it allows for a ton of code re-use. If we want the same `SearchBar` to appear in ten different places on the website, we don't have to rewrite the code for it ten times - we just have to insert the `<SearchBar />` component anywhere we need it!

Also - you'll notice that when we write out the `<SearchBar />` component that we include a `/` at the end. This is because our React elements are always **self-closing**. Just like in HTML and JSX, any time we create a component that doesn't have any children, we let React know by adding a `/`.

#### Component kitchen - cook 'em up!
Practice making a few new components of your own choosing and nesting them inside each other. They can do whatever you want - this is just to practice and get used to the class component syntax.

### Styling in React 
There are lots of opinions on the best way to style React components. Inline styling, one big CSS file, a CSS file for each component, a library like [CSS Modules](https://github.com/css-modules/css-modules) or [any of these other ones](https://github.com/MicheleBertoli/css-in-js#features).

CSS-preprocessors further complicate that discussion.

**We are only going to require CSS files in the bootcamp.**

For your projects, we do not allow inline styling and require that there be only one CSS file. How you get there is up to you.

#### Sass and Create React App
In order to use Sass when working with Create React App, we need to add a few things.  You can find a write up of this in [the documentation for Create React App](https://facebook.github.io/create-react-app/docs/adding-a-sass-stylesheet#docsNav). 

<!-- 
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

But you can do whatever you want! -->
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

#### Animations and transitions
To animate components, the React documentation suggests [React Motion](https://github.com/chenglou/react-motion) and [React Transition Group](https://reactcommunity.org/react-transition-group/).

### Additional Resources
* [React for Beginners](https://reactforbeginners.com/) (taught by Juno instructor Wes Bos!)
* [Learning React: Getting Started and Concepts](https://scotch.io/tutorials/learning-react-getting-started-and-concepts)
* [Hello World in React](http://codepen.io/gaearon/pen/ZpvBNJ?editors=0010) (a CodePen you can play around with)
