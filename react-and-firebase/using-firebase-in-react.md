<!-- Student takeaways: -->
<!-- At the end of this lesson, students should be able to:
- Add data to a Firebase database manually AND using .push()
- Retreive data from a Firebase database using .on('value')
- Delete data using .remove()
 -->
# Getting Started with Firebase and React
## React and Firebase
Earlier on, we learned how to add Firebase to our jQuery to-do app so that we could hold on to our to-dos, even after page refresh.

We're now going to learn how to add Firebase to a React project so that our applications can have their own database/back end.

Having a database for our application opens up a ton of possibilities for the kinds of applications we can build; our apps can have users, and each one of those users can have a customized experience interacting with our website based on their preferences.

### Setting up Firebase
As always, the first thing that we'll need to do is create a new project inside our Firebase dashboard.

1. Head over to <https://firebase.google.com> and click 'Go to console' in the top right corner.
  ![Firebase console](https://hychalknotes.s3.amazonaws.com/01-create-project-firebase-console.png)
2. Click 'Add Project'.

3. Give your new project a name and click 'Create Project'.
  ![Firebase console](https://hychalknotes.s3.amazonaws.com/02-name-project-firebase.png)

4. Click 'Add Firebase to your web app' or the `</>` icon. This will give you the embed code to add Firebase to your project.
  ![Firebase config image](https://hychalknotes.s3.amazonaws.com/06-firebase-config.png)

5. You're now ready to hook your React project up to Firebase. Create a new app by running  `create-react-app bookshelf`.

6. We will also need to install `firebase` , run `npm install firebase` 

7. In your `src` folder create a filed `firebase.js` and add the following lines
```javascript
//firebase.js
import firebase from 'firebase';

// Initialize Firebase
//USE YOUR CONFIG OBJECT
const config = {
	apiKey: "AIzaSyAs8R3gyKI9pnUyls5jwruEPGlUoTC1RJE",
	authDomain: "fir-bookshelf-8d68a.firebaseapp.com",
	databaseURL: "https://fir-bookshelf-8d68a.firebaseio.com",
	projectId: "fir-bookshelf-8d68a",
	storageBucket: "fir-bookshelf-8d68a.appspot.com",
	messagingSenderId: "548100999451"
};
firebase.initializeApp(config);

// this exports the CONFIGURED version of firebase
export default firebase;
```

### Getting data from Firebase
Let's imagine that we were building a digital bookshelf that kept track of all of our favourite books. To start, let's add some data to our Firebase database.

In your Firebase console, click the 'Database' tab. We're giong to create a realtime database in text mode. When you get through, you should see a screen that looks something like this:
![Firebase database tab](https://hychalknotes.s3.amazonaws.com/firebase-database-screenshot.png)

Let's add some books to our bookshelf. Click the plus next to the name of our database and let's add some lines with your favourite books:

```
book1: "Beloved"
book2: "The Hitchhiker's Guide to the Galaxy"
book3: "A Little Life"
```

Now that we have some data, let's build a little React app that can grab it. We'll import `firebase` into the `App.js` component and set up an initial `book` state.

```javascript
//App.js
import React, { Component} from 'react';
import firebase from './firebase';

class App extends Component {
  render() {
    return (
      <div></div>
    )
  }
}
```

In React, when we grab data from external sources to be used in our app, we need to store that information. Typically, we stored it in our component's state.

Let's prepare our state to receive some book data and tell our `render` method what to do with the books data once we've got it:

```javascript
//App.js
class App extends Component {
  constructor() {
    super();
    this.state = {
      books: []
    }
  }
  render() {
    return (
      <ul>

      return(
        {this.state.books.map((book) => {
          <li>{book}</li>
        })}
      )
      </ul>
    )
  }
}
```

Now our component will map through our `books` array, grabbing any books it finds in there and display them as a list on the page.

All that's left to do is grab our data from Firebase. We'll do this by using the `componentDidMount` lifecycle hook to call for the data we want and store it in state.

```javascript
//App.js
class App extends Component {
 // ...rest of our code here
 componentDidMount() {
   const dbRef = firebase.database().ref();
   dbRef.on('value', (response) => {
     console.log(response.val());
   });
 }
}
```

If this worked successfully, you should see your books appear as an object in the console!

Let's break down what's happening here:

1. `dbRef = firebase.database().ref()`: First, we create a variable called `dbRef` and point it towards our Firebase database.

2. `dbRef.on('value', (response) => {`: Second, we add an event listener to the variable that will update us on changes to our database and provide us a callback function to directly access the data from our database (here we named the parameter `response`).

3. `console.log(response.val())`  : Third, we use the `val()` method to grab our database information and print it out into the console.

### Storing Firebase data in state

Now that we're seeing our data, we need to store it in the state. Let's update our `componentDidMount` function to do that:

```javascript
//App.js
const dbRef = firebase.database().ref();
dbRef.on('value', (response) => {
  const newState = [];
  const data = response.val();

  for (let key in data) {
    newState.push(data[key]);
  }

  this.setState({
    books: newState
  });

});
```

There's a lot of new code here, so let's break down exactly what we're doing:

1. `const newState = []` : When we set set (or re-set) the state of our component, we need to create a variable that will store the new state we want to introduce to our app.

2. `const data = response.val()`: Here we store our response inside of a `data` variable so that it's easier to reference later

3. `for (let key in data) {`: We need to iterate through our `data` object so that we can grab all the book names out of it!

4. `newState.push(data[key]);`:  We push all of the books into our `newState` array, which is a temporary array we only need inside this function.

5. `this.setState({ books: newState });` : We call `this.setState` in order to update our component's state with our `newBooks` array.

If this worked successfully, you'll notice that the book titles are now appearing on the page! You'll also notice if you go into your database and add a new book, it will appear on the page. Dang!

## Updating data
Now we're able to successfully retrieve and display information from our database, but we still don't have a way to add new books to our bookshelf. Let's add that functionality now!

We'll need to add an input and a book-adding button to our `App` component:

```js
//App.js
class App extends Component {
  constructor() {
    super();
    this.state = {
      books: []
    }
  }
    render() {
      return (
        <div>
          <ul>
          {this.state.books.map((book) => {
            return (
              <li>
                {book}
              </li>
            )
          })}
          </ul>
          <form action="submit>
            <input type="text" placeholder="Add a book to your bookshelf" />
            <button>Add Book</button>
          </form>
        </div>
      )
    }

    componentDidMount() {
      // ....
    }
}
```

Now we have an input and a button, but they currently don't do anything! Let's start by attaching a `handleChange` method to store information about what the user is typing into the input field within our state:

```javascript
//App.js
constructor() {
  super();
  this.state = {
    books: [],
    userInput: ''
  }
}

handleChange = (event) => {
  this.setState({userInput: event.target.value})
}

render() {
  return (
    <div>
      <ul>
      {this.state.books.map((book) => {
        return (
          <li>
            {book}
          </li>
        )
      })}
      </ul>

    <form action="submit>
      <input type="text" onChange={this.handleChange} placeholder="Add a book to your bookshelf" />
      <button onClick={this.handleClick}>Add Book</button>
    </form>
    </div>
  )
}
```
What's going on here?

1. We've attached the `handleChange` method to our input field.

2. It will be triggered any time the field is "changed" – that is, whenever the user types in it.

3. Every time this happens, React updates the state of our `App` component to be equal to whatever is currently in the input field.

We can see exactly how this is working with a quick glance at the React dev tools. You'll see that `this.state.userInput` is being updated dynamically as you type in the text field!

Now let's add our `handleClick` method:

```javascript
//App.js
constructor() {
  // ..
}

handleChange(event) {
  // ..
}

handleClick(e) {
  e.preventDefault();
  const dbRef = firebase.database().ref();
  dbRef.push(this.state.userInput);
  this.setState({userInput: ""})
}

render() {
  return (
    <div>
      { /* ... */ }
      <input type="text" onChange={this.handleChange} placeholder="Add a book to your bookshelf" />
      <button onClick={this.handleClick}>Add Book</button>
    </div>
  )
}
```

Our `handleClick` function is only four lines, but they are important ones:

1. `e.preventDefault` prevents the default action of form submission.
1. `const dbRef = firebase.database().ref();` : First, as usual, we grab our reference to the current database.

1. `dbRef.push(this.state.userInput);` : We grab whatever the current value of `this.state.userInput` is (this will be whatever the user has typed in the input field), and push that into the database.

1. `this.setState({userInput: ' '})` : We reset the state of `userInput` to an empty string, effectively clearing the input.

We're almost there! Now we have to be able to remove the data.

## Removing data
We now have the ability to add new books to and retrieve existing books from our database – the final step is to add the ability to remove books from our bookshelf.

If we go back and look at our database in the Firebase dashboard, we can see that all of our data is stored as key-value pairs in a structure very similar to an object.

Each book has a corresponding key. We can tell Firebase which book we want to remove using the book's key.

The first thing we'll need to do is change the structure of the data that we're currently getting back from Firebase. Right now, we grab each one of the books from our database and store it in an array as a series of strings, like this:

`["A Little Life", "Beloved"]`

So, right now, we aren't storing any reference to each one of these books' unique keys. Let's modify our data so we can get the key as well and store it.

We'll need to modify our `componentDidMount` lifecycle hook:

```javascript
//App.js
componentDidMount() {
      // ...
      for (let key in data) {
        newState.push({key: key, name: data[key]});
      }

      //...
}
```

Now, instead of pushing a string, we're pushing in an object with two properties:

1. a key, which refers to the unique id of the book inside the Firebase database
and
2. the actual book title

This means that we're going to store an array of object, rather than an array of strings, inside of `this.state.books`, so we'll need to modify our `render` method to reflect this:


```javascript
//App.js
render() {
    return (
      <div>
        <ul>
        {this.state.books.map((book, i) => {
          return (
            <li key={i}>
              {book.name} - {book.key}
            </li>
          )
        })}
        </ul>
        <form actions="submit">
          <input type="text" placeholder="Add a book to your bookshelf" value={this.state.value} onChange={this.handleChange} />
          <button onClick={this.handleClick}>Add Book</button>
        </form>
      </div>
    )
  }
```

Now that we're grabbing our book ID, we need to add a 'Remove' button that has a click event on it that will tell Firebase which ID we want to remove:

```javascript
//App.js
<li key={i}>
  {book.name} <button onClick={() => this.removeBook(book.key)}> Remove </button>
</li>
```

The reason that we use `() => this.removeBook(book.key)` here is that we are passing a **reference** to a function rather than **calling** the function. If this is confusing for you right now don't worry about it too much, just remember that you may need to do this in order to pass data from your component!

Now let's write our `removeBook` function inside our `App` component:

```javascript
//App.js
removeBook(bookId) {
  const dbRef = firebase.database().ref(bookId);
  dbRef.remove();
}
```

In this function, we are:
1. Grabbing a reference to our database. By passing in the specific `bookId` we sent up from inside of our `render` method, we can grab the specific book that the user wants to remove.

2. Remove that item from the database by calling `.remove()`

You'll notice that your app automatically updates to remove that item from your page! This is because of the `.on('value')` event listener!

## Additional Resources
* [Firebase Documentation](https://firebase.google.com/docs/web/setup)
