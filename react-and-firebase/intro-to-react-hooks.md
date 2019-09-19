<!-- Student takeaway: -->
<!--Student will be able to:
- Understand how to use useState
- Understand how to use useEffect in it's simplest context
- Change a class component with state and lifecycle methods to a function component
- know where resources are to investigate further
 -->

# Intro to React Hooks

React Hooks make it possible to use state and lifecycle methods in Function components therefore eliminating the need for Class components. But don't worry there is no plans to remove Class components from the spec.

They also make it possible to reuse stateful logic by making our own hooks. 

React introduced Hooks in 2018 to solve some problems that the React team had come up against while maintaining the React codebase for 5 years. 

1. Classes are difficult to understand (and take a lot of computer power to process).
2. App.js gets big and confusing with business logic that could be more reusable and componentized. 


## Using State in a Function Component

React Hooks includes a built-in Hook called `useState` that allows us to use state in a Function component. `useState` is a function that accepts one parameter which sets the starting value of the state we want to declare. It returns an array of 2 items - the first is the variable we are declaring and the second is a function that we can use to update that specific piece of state. 

Using array destructuring, we can name those two returned items for use in our code. 

Let's look at it once and then break down the pieces.

First, we have to import `useState` from the react library.

```jsx
import React, { useState } from 'react';
```

Then we can use it like this:

```jsx
const [likes, setLikes] = useState(0);
```

We are creating a variable to hold the return value of useState, which is an array of 2 items. 

We are naming the first item `likes`, it will be the name of the piece of state we want to access.

The `0` value in `useState(0)` sets the initial state of `likes` to 0. This is the same as doing:

```jsx
this.state({
    likes: 0,
})
```
The second value in the destructed array is naming the function that we will use to update the likes 'setLikes'. This function will replace the use of `this.setState()`. When we call `setLikes`, we will pass in the new value of the `likes` state as a parameter.


## Updating a Class component to a Function Component

When we define state in a Class component we do it like this:

```jsx
class App extends Component {
  componentDidMount(){
    super();
    this.state = {
        likes: 0
    }
  }
  addLike = () =>{
      this.setState({
          likes: this.state.likes + 1
      })
  }
  render() {
    return (
        <div>
            Likes: {this.state.like}
            <button onClick={this.addLike}>♥️</button>
        </div>
    ) 
  }
}
```

Now we can change it to look like this:

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

👀👀👀👀👀👀👀👀👀👀👀
Cool.

### Calling useState() multiple times
We can call `useState()` as many times as we like within our components for different pieces of state.

```jsx
const [likes, setLikes] = useState(0);
const [currentUser, setCurrentUser] = useState('Guest');
const [musicList, setMusicList] = useState(['The Beatles', 'War on Drugs', 'Florence and the Machine']);
```

## Using Lifecycle methods in a Function Component

We can also use lifecycle methods in a Function component using a built-in Hook called `useEffect`. 

`useEffect` is like `componentDidMount`, `componentDidUpdate` and `componentWillUnmount` combined. It is called after the first render and after every update. 

We load it in from React the same way we load in useState.

```jsx
import React, { useState, useEffect } from 'react';
```

Then we can start to use it within our Function component. `useEffect` accepts a callback function as parameter that contains the code that we want to execute after every render. 

```jsx
function App(){
    useEffect(() => {
        console.log('hello');
    })
}
```

We probably want to do something more interesting than console.log though. `useEffect` is a great place to make API calls, connect to Firebase or subscribe to some external information. 

```jsx
useEffect(() => {
    const dbRef = firebase.database().ref();
        dbRef.on('value', (snapshot) => {
            const database = snapshot.val();
            setMessages(database)
        })
    })
```

However, there was a reason that we made these API calls in componentDidMount rather than in componentDidUpdate. We were relying on the componentDidMount method to only run once. If we run the code above, we will run into an infinite loop error because we setting the state after every render which is causing the component to rerender.. which is causing the component to rerender...which is causing the component to rerender...

<!-- IMAGE OF THE ERROR MESSAGE -->

To remedy this, we can add an empty array as the second argument to `useEffect`. This argument is a list of properties which the useEffect function will compare against current state and props to check if it should call the effect. If we pass it an empty array, then it knows it will never have to rerun because it has no dependancies. 

```jsx
useEffect(() => {
    const dbRef = firebase.database().ref();
        dbRef.on('value', (snapshot) => {
            const database = snapshot.val();
            setMessages(database)
        })
    }, [])
```
<!-- 
- using effects in order (why they can't be in conditionals - put conditionals in the effect)
- this is just javascript -->


## Excercise
App.js to Functional Component

## Next Steps
Make your own hook

## Additional Resources 
React Hooks Documentation


