<!-- Student takeaway: -->
<!--Student will:
- Understand how to use useState
- Understand how to use useEffect in it's simplest context
- Be able to change a class component with state and lifecycle methods to a function component
- Know where resources are to investigate further
 -->

# Intro to React Hooks

React Hooks are special functions provided by React that make it possible to "hook into" state and lifecycle methods in function components. React introduced Hooks in 2018 to solve some problems that the team had come up against while maintaining the React codebase for 5 years:

1. Classes can be difficult to understand (and take a lot of computer power to process).
2. `App.js` gets big and confusing with business logic that could be more reusable and componentized. 

Hooks eliminate the need for class components. (But Hooks are totally backwards compatible and there are no plans to remove class components from the spec.) 

## Using state in a function component
React Hooks includes a built-in Hook called `useState` that allows us to create and update state. `useState` is a function that accepts one argument: the starting value of the state we want to declare. The `useState` function returns an array of 2 items: 
1. a single variable that will represent a piece of state
2. a function that we can use to update that specific piece of state 

To use `useState`, we have to import `useState` from the React library.

```jsx
import React, { useState } from 'react';
```

We can name the two values returned from the `useState` function with array destructuring:
```jsx
const [likes, setLikes] = useState(0);
```

Here, we are creating a variable to hold the return value of useState, which is an array of 2 items. We are naming the first item `likes`, which will be the name of the piece of state we want to access.

The second value in the destructured array names the function that we will use to update the `likes` value in state. In this case we have named it `setLikes`. This function will replace the use of `this.setState()`. When we call `setLikes`, we will pass in the new value of the `likes` state as an argument.

Instead of this 👎
```
this.setState({
    likes: 4,
});

```

Try this 👍
```
setLikes(4);

```


| Class Components | Function Components  |
| ---------------- | ------------------- |
| `this.setState({ `| `setLikes(4);`       |
|      `likes: 4,`  |                     |
|  `});`            |                     |


<table>
    <tr>
        <th>
            Class Components
        </th>
        <th>
            Function Components
        </th>
    </tr>
    <tr>
        <td>
<pre>
    this.setState({
        likes: 4,
    });
</pre>
        </td>
        <td>
<pre>
    setLikes(4);
</pre>
        </td>
    </tr>
</table>

The `0` value in `useState(0)` sets the initial state of `likes` to 0. This is the same as doing:

```jsx
this.state = {
    likes: 0,
}
```




## Refactoring a class component to a function component using Hooks

Consider this class component:
```jsx
class App extends Component {
  constructor(){
    super();
    this.state = {
        likes: 0
    }
  }
  addLike = () => {
      const newLikes = this.state.likes;
      this.setState({
          likes: newLikes + 1
      })
  }
  render() {
    return (
        <div>
            Likes: {this.state.likes}
            <button onClick={this.addLike}>♥️</button>
        </div>
    ) 
  }
}
```

Using Hooks, that same component looks like this:
```jsx
function App() {
    const [likes, setLikes] = useState(0);
    return (
        <div>
            Likes: {likes}
            <button onClick={() => setLikes(likes + 1)}>♥️</button>
        </div>
    ) 
  }
}
```

👀👀C👀👀O👀👀O👀👀L👀👀👀


### Calling useState() multiple times

We can call `useState()` as many times as we like within our components for different pieces of state.

```jsx
const [likes, setLikes] = useState(0);
const [currentUser, setCurrentUser] = useState('Guest');
const [musicList, setMusicList] = useState(['The Beatles', 'War on Drugs', 'Florence and the Machine']);
```

Now our state object has three keys on it - 'likes', 'currentUser', and 'musicList'. You could visualize it like this: 

```jsx
this.state = {
    likes: 0,
    currentUser: 'Guest',
    musicList: ['The Beatles', 'War on Drugs', 'Florence and the Machine']
}
```

## Using lifecycle methods in a function component
React Hooks includes a built-in Hook called `useEffect` that allows us to hook into a component's lifecycle methods.

`useEffect` is like `componentDidMount`, `componentDidUpdate` and `componentWillUnmount` combined. It is called after the first render and after every update. 

We load it in from React the same way we load in `useState`:
```jsx
import React, { useState, useEffect } from 'react';
```

`useEffect` accepts [a callback function](https://github.com/HackerYou/bootcamp-notes/blob/master/applied-javascript/how-do-callbacks-work.md) as an argument. 

```jsx
function App(){
    useEffect(() => {
        console.log('hello');
    })
}
```

We probably want to do something more interesting than `console.log`. `useEffect` seems like a great place to make API calls, connect to Firebase, or subscribe to some external information. 

```jsx
//setting a `message` key on our state object
const [message, setMessage] = useState('');
useEffect(() => {
    axios({
        method: 'get',
        url: 'https://8ball.delegator.com/magic/JSON/Are showers a mandatory thing?',
    }).then((res) => {
        //here we update the `message` key in state
        setMessage(res);
    });
})
```

And it is! But there was a reason that we made these API calls in `componentDidMount` rather than in `componentDidUpdate`. The `componentDidMount` method usually only runs once. 

If we run this code, we will run into an infinite loop error because we are **setting the state after every render** which is causing the component to rerender... which is causing the component to rerender... which is causing the component to rerender...

<!-- IMAGE OF THE ERROR MESSAGE -->
![Infinite loop error message](https://hychalknotes.s3.amazonaws.com/infinite-loop-screenshot--bootcamp.png)

To remedy this, we can pass an empty array as an *optional second argument* to `useEffect`. This optional second parameter expects an array of properties that the `useEffect` function will compare against current state and props to check if it should run the callback function. 

Passing an empty array means it will never have to rerun because it has nothing to check against. 

#### TL;DR
Add an empty array as the second argument to the `useEffect` hook in order to only run it once, thus acting like `componentDidMount`.

```jsx
const [message, setMessage] = useState('');
useEffect(() => {
    axios({
        method: 'get',
        url: 'https://8ball.delegator.com/magic/JSON/Are showers a mandatory thing?',
    }).then((res) => {
        setMessage(res);
    });
//👇 this is where we add the empty array
}, []);
```

### Calling useEffect() multiple times

Just like `useState`, we can call `useEffect` multiple times within a component. This allows us to separate different code functionality into different instances of `useEffect` making our code more modular. When React runs the code, it keeps track of the order in which each `useEffect` is called. For this reason, we can't call `useEffect` from inside a conditional statement. Instead, we will conditionally run code inside of `useEffect`.

Incorrect 👎
```jsx
if(currentUser === 'Guest'){
    useEffect(() => {
            console.log('The current user is Guest.')
    });    
}  
```

Correct 👍
```jsx
useEffect(() => {
    if(currentUser === 'Guest'){
        console.log('The current user is Guest.')
    } 
});      
```

## React Hooks in the Wild
React recommends that companies start using Hooks when they are ready but not to rewrite all of the components in their codebase at once. Hooks will most likely become widely used over the next couple of years.  But you have the chance to be an expert at your workplace because it is new to everyone. Use what you are comfortable with and adopt more React Hook functionality as you gain confidence and understanding.


## Exercise
1. Let's download [this folder](https://hychalknotes.s3.amazonaws.com/learning-hooks.zip).
2. Navigate to the file in your terminal. Then run `npm install` and `npm start` to open the site in your browser. 
3. In the App.js file, change `App` from a class component to a functional component using `useState` and `useEffect`. 


## Next Steps


1. Because Hooks are functions, you can write your own!

> Imagine writing a handleClick function that manipulates the state in your `App.js` component. Instead of passing it down through the component tree, you can write a hook for it and import that hook into the components that need to manipulate that piece of state.

Check out the React Hooks [Build Your Own Hooks](https://reactjs.org/docs/hooks-custom.html) documentation to learn more.

2. There are many more built-in Hooks available!

| Hook | Functionality  |
|---|---|
|`useContext` | lets you read the context object and subscribe to its changes. [More about the Context API](https://reactjs.org/docs/context.html) |
| `useReducer`  | is preferable to `useState` when you have complex state logic that involves multiple sub-values or when the next state depends on the previous one |
|  `useMemo` | Returns a memoized value --> memoization stores the results of expensive function calls and returns the cached result when the same inputs occur again |
|  `useCallback` | Returns a memoized callback  |
|  `useRef` |  useRef returns a mutable ref object. [More about using refs](https://reactjs.org/docs/refs-and-the-dom.html)|

Take a look at the [Hooks API](https://reactjs.org/docs/hooks-reference.html) documentation to find even more built-in hooks.

## Additional Resources 
[React Hooks documentation](https://reactjs.org/docs/hooks-intro.html)


