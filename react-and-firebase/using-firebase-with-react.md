<!-- Student takeaways: -->
<!-- At the end of this lesson, students should be able to:
- Add data to a Firebase database manually AND using .push()
- Retreive data from a Firebase database using .on('value')
- Delete data using .remove()
 -->
# Using Firebase with React

## React and Firebase
Earlier on, we learned how to add Firebase to our jQuery to-do app so that we could hold on to our to-dos, even after page refresh.

We're now going to learn how to add Firebase to a React project so that our applications can have their own databases.

Having databases for our applications opens up a ton of possibilities for the kinds of applications we can build; our apps can have users, and each one of those users can have a customized experience interacting with our website based on their preferences.

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

6. We will also need to install `firebase` , run `npm install firebase --save` 
  * The `npm install` command downloads files. If you go into your `node_modules` folder, you should see a folder called `firebase`.
7. In your `src` folder create a filed `firebase.js` and add the following lines
```javascript
//firebase.js
import firebase from 'firebase';

// Initialize Firebase
//USE YOUR CONFIG OBJECT
const config = {
	apiKey: "YOUR-API-KET",
	authDomain: "bookshelf-8d68a.firebaseapp.com",
	databaseURL: "https://bookshelf-8d68a.firebaseio.com",
	projectId: "bookshelf-8d68a",
	storageBucket: "bookshelf-8d68a.appspot.com",
	messagingSenderId: "548100999451"
};
firebase.initializeApp(config);

// this exports the CONFIGURED version of firebase
export default firebase;
```

### Getting data from Firebase
Let's imagine that we were building a digital bookshelf that kept track of all of our favourite books. To start, let's add some data to our Firebase database.

1. In your Firebase console, click the 'Database' tab. We're going to create a **realtime database** in. Firebase REALLY wants you to make a Cloud Firestore one right now. Do not do that. Scroll past it until you see something like this:
![Firebase database tab](https://hychalknotes.s3.amazonaws.com/07-firebase-database-screenshot.png)

1. Hit 'Create database'.
1. Start in test mode.

Let's add some books to our bookshelf. Click the '+' next to the name of your database and add some lines with your favourite books:

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
   // here we create a variable that holds a reference to our database
   const dbRef = firebase.database().ref();
   // here we add an event listener to that variable that will fire every time there is a change in the database
   // this event listener takes a callback function which we will use to get our data from the database and call it response
   dbRef.on('value', (response) => {
     // here we use Firebase's .val() method to parse our database info the way we want it
     console.log(response.val());
   });
 }
}
```

If this worked successfully, you should see your books appear as an object in the console!

### Storing Firebase data in state

Now that we're seeing our data, we need to store it in the state. Let's update our `componentDidMount` function to do that:

```javascript
//App.js
const dbRef = firebase.database().ref();
dbRef.on('value', (response) => {
  // Here we're creating a variable to store the new state we want to introduce to our app
  const newState = [];
  // Here we store the response from our query to Firebase inside of a variable called data
  // .val() is a Firebase method that gets us the information we want
  const data = response.val();

  //data is an object, so we iterate through it using a for in loop to access each book name 
  for (let key in data) {
    // inside the loop, we push each book name to an array we already created inside the .on() function called newState
    newState.push(data[key]);
  }

 // then, we call this.setState in order to update our component's state using the local array newState
  this.setState({
    books: newState
  });

});
```

If this worked successfully, you'll notice that the book titles are now appearing on the page! You'll also notice if you go into your database and add a new book, it will appear on the page. Dang!

## Updating data
Now we're able to successfully retrieve and display information from our database, but we still don't have a way to add new books to our bookshelf. Let's add that functionality now!

> Remember that you always use `.setState()` to change state after it's been initialized, never `this.state = `.

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
                  <p>{book}</p>
                </li>
              )
            })}
          </ul>
          <form action="submit">
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

// this event will fire every time there is a change in the input it is attached to
handleChange = (event) => {
  // we're telling React to update the state of our `App` component to be equal to whatever is currently the value of the input field
  this.setState({userInput: event.target.value})
}

render() {
  return (
    <div>
      <ul>
      {this.state.books.map((book) => {
        return (
          <li>
            <p>{book}</p>
          </li>
        )
      })}
      </ul>

    <form action="submit">
      { /* Here, we've attached the `handleChange` method to our input field.*/}
      <input type="text" onChange={this.handleChange} placeholder="Add a book to your bookshelf" />
    { /* Here, we've attached the `handleClick` method to our input button.*/}
      <button>Add Book</button>
    </form>
    </div>
  )
}
```
We can see exactly how this is working with a quick glance at the React dev tools. You'll see that `this.state.userInput` is being updated dynamically as you type in the text field!

Now, let's make sure React always knows about the changes in our input field by _controlling_ (sometimes called _binding_) our text input:

```javascript
//App.js
constructor() {
  super();
  this.state = {
    books: [],
    userInput: ''
  }
}
// ...
render() {
  return (
    <div>
      <ul>
      {this.state.books.map((book) => {
        return (
          <li>
            <p>{book}</p>
          </li>
        )
      })}
      </ul>

    <form action="submit">
    {/* add the value attribute and set it's value equal to whatever's in state*/}
      <input type="text" onChange={this.handleChange} placeholder="Add a book to your bookshelf" value={this.state.userInput} />
      <button>Add Book</button>
    </form>
    </div>
  )
}
```
Here, we're using [the HTML attribute `value`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Input#value) to set the intial state of the input and we're using `this.state.userInput` to keep track of it as it changes.

Now let's add our `handleClick` method:

```javascript
//App.js
constructor() {
  // ..
}

handleChange(event) {
  // ..
}

handleClick(event) {
  //event.preventDefault prevents the default action: form submission
  event.preventDefault();
  // here, we create a reference to our database
  const dbRef = firebase.database().ref();
  // here we grab whatever value this.state.userInput has and push it to the database
  dbRef.push(this.state.userInput);
  // here we reset the state to an empty string
  this.setState({userInput: ""})
}

render() {
  return (
    <div>
      { /* ... */ }
      <input type="text" onChange={this.handleChange} placeholder="Add a book to your bookshelf" value={this.state.userInput} />
      <button onClick={this.handleClick}>Add Book</button>
    </div>
  )
}
```

We're almost there! Now we have to be able to remove the data.

## Removing data
We now have the ability to add new books to and retrieve existing books from our database – the final step is to add the ability to remove books from our bookshelf.

If we go back and look at our database in the Firebase dashboard, we can see that all of our data is stored as key-value pairs in a structure very similar to an object.

Each book has a corresponding key. We can tell Firebase which book we want to remove using the book's key.

The first thing we'll need to do is change the structure of the data that we're currently getting back from Firebase. Right now, we grab each one of the titles of the books from our database and store it in an array as a atring, like this:

`["A Little Life", "Beloved"]`

So, right now, we aren't storing any reference to each one of these books' unique keys. Let's modify our data so we can get the key as well and store it.

We'll need to modify our `componentDidMount` lifecycle method:

```javascript
//App.js
componentDidMount() {
      // ...
      for (let key in data) {
        // 
        newState.push({key: key, name: data[key]});
      }

      //...
}
```

Log the two values we get inside the loop. What are they?

1. `key` refers to the unique ID of the book stored in the Firebase database.
2. `data[key]` refers to the associated book title stored in Firebase.

This means that we're going to store an array of objects, rather than an array of strings, inside of `this.state.books`, so we'll need to modify our `render` method to reflect this:

```javascript
//App.js
render() {
    return (
      <div>
        <ul>
        {this.state.books.map(book => {
          return (
            <li key={book.key}>
              <p>{book.name} - {book.key}</p>
            </li>
          )
        })}
        </ul>
        <form actions="submit">
          <input type="text" onChange={this.handleChange} placeholder="Add a book to your bookshelf" value={this.state.userInput} />
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

The reason that we use `() => this.removeBook(book.key)` here is that we are passing a **reference** to a function rather than **calling** a function. If this is confusing for you right now don't worry about it too much, just remember that you may need to do this in order to pass data from your component!

> You can think of this syntax `{ ()=> someFunction(information) }` as saying "Wait a second! I have some information to give `someFunction()` before it runs!"

Now let's write our `removeBook` function inside our `App` component:

```javascript
//App.js
// this function takes an argument, which is the ID of the book we want to remove
removeBook(bookId) {
  // here we create a reference to the database AT THE BOOK'S ID
  const dbRef = firebase.database().ref(bookId);
  // using the Firebase method .remove(), we remove that node
  dbRef.remove();
}
```

You'll notice that your app automatically updates to remove that item from your page! This is because we initialized the `.on('value')` event listener when the app is created. `.on('value')` fires every time there is a change to a value in the database.

## Additional resources
* [Firebase documentation](https://firebase.google.com/docs/web/setup)
* [React documentation about what controlled inputs are and how to control inputs other than text](https://reactjs.org/docs/forms.html#controlled-components)