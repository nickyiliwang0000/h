<!-- Student takeaway -->
<!-- By the end of this lesson, the student should know:
- How to change their database rules to allow only authenticated users to write to/read
- Create a conditionally rendering button for login/logout
- Use Firebase's Google authentication method to sign in
- Use Firebase's Google authentication method to sign out
- Use onAuthStateChange to persist data after refresh
-->

# Authentication with Firebase

Twitter, Facebook, even Slack - all of these applications have one thing in common: they all employ authentication. You create an account using your e-mail and password, log in, and enjoy a personalized experience in those applications. From a technical standpoint, this movement through the application is often called the _authentication flow_ or simply _authentication_.

### How we used to do it
In the past, authentication was tricky. It required understanding how databases work, more advanced computer science concepts like tokenization, and a solid understanding of a back-end programming language like PHP or Ruby.

### How we can do it now
Firebase offers us a suite of authentication tools we can use to store our user information in their databases. Using Firebase's authentication toolkit, we'll be learning how to:

* Create a user with e-mail and address
* Allow the user to sign in
* Allow the user to log out
* Allow the user's session to persist (a.k.a. for them to remain logged in even after the page refreshes, or they navigate away and come back)

Let's dive in!

## Creating a simple application with authentication
We're going to create a simple application that allows us to create a user and allows that user to log in and log out. We are intentionally keeping this as straightforward as possible so that it will be easier to integrate into your existing applications.

### Setup
1. Start by creating a new React project: `create-react-app authentication-example`. NPM install `firebase` as well by running `npm install firebase`
2. In the Firebase dashboard, create a new project. Call it `firebase-react-authentication`. Click on the 'Authentication' tab, and then click 'Set Sign-Up Method'. Toggle 'enable Google authentication' and click save.

3. Grab the initialization code and add it to your `app.js`. It should look something like this:


```javascript
// App.js
import firebase from firebase;

var config = {
  apiKey: "YOUR-API-KEY",
  authDomain: "fir-react-authentication.firebaseapp.com",
  databaseURL: "https://fir-react-authentication.firebaseio.com",
  storageBucket: "fir-react-authentication.appspot.com",
  messagingSenderId: "179937455676"
};
firebase.initializeApp(config);
```

### Writing our first component
4. Let's set up our first component:
```javascript
//App.js
import React from 'react';
import ReactDOM from 'react-dom';

class App extends React.Component {
  render() {
    return (
      <div>
      </div>
    )
  }
}

ReactDOM.render(<App />, document.getElementById('app'))
```

We're going to use Google as our authentication provider for this project, primarily because it will make handling our authentication flow very simple: we won't have to worry about things like error handling and password validation since Google will take care of all of that for us. We also won't have to build any UI components (other than a login and log out button) to handle authentication. Everything will be managed through a pop-up.

In past versions of our Firebase apps, we've configured them so **anyone** can read and write to the database. We're going to change this so that only users who are signed in can write to the database. Change your rules at 'Database' > 'Rules' and hit 'Publish' so that it the rules look like this: 

```JSON
{
  "rules": {
    ".read": "auth != null",
    ".write": "auth != null"
  }
}
```

These rules tell Firebase to only allow users who are authenticated to read and write from the database.

We are going to create an instance of the Google provider object as well as an instance of the auth module from firebase:
```javascript
//App.js
const provider = new firebase.auth.GoogleAuthProvider();
const auth = firebase.auth();
```

Now, inside your app's constructor, let's start by carving out a space in our initial state that will hold all of our signed-in user's information.

```javascript
//App.js
constructor() {
    super();
    this.state = {
      user: null
    }
```

Let's set up some buttons to render conditionally whether or not a user is logged in our out.

```javascript
 render() {
    return (
      <div className="App">
        <header>
          <h1>Authy App</h1>
          {this.state.user ? <button onClick={this.logout}>Log Out</button> : <button onClick={this.login}>Login</button>}</header>     
      </div>
    );
  }
```

If the value of `this.state.user` is truthy, that means the user is currently logged in and should see the log**out** button. If the value of `this.state.user` is null, that means the user is currently logged out and should see the log **in** button.

The `onClick` of each of these buttons will point to two functions that we will create in the component itself in just a second: `login` and `logout`.

Now, we can set up the `login` method to handle our Google authentication. 

```javascript
login = () => {
  auth.signInWithPopup(provider) 
    .then((result) => {
      const user = result.user;
      this.setState({
        user
      });
    });
}
```

`signInWithPopup` has a promise API that allows us to call `.then` on it and pass in a callback. This callback will be provided with a `result` object that contains, among other things, a property called `user`. This property has all the information about the user who has just successfully signed in - including their name and user photo. We then store this inside of the state using `setState`.

Try signing in and then checking the React DevTools - you'll see the user there!

The `logout` method is incredibly straightforward. After the login method inside your component, add the following method:

```javascript
logout  = () => {
  auth.signOut()
    .then(() => {
      this.setState({
        user: null
      });
    });
}
```

### Persisting login across refresh

Right now, every time you refresh the page, your application forgets that you were already logged in, which is a bit of a bummer. Firebase has an event listener called `onAuthStateChange` that can check every single time the app loads to see if the user was already signed in last time they visited your app. If they were, you can automatically sign them back in.

We'll use this event listener inside of our `componentDidMount`, which is meant for these kinds of tasks:

```javascript
componentDidMount() {
  auth.onAuthStateChanged((user) => {
    if (user) {
      this.setState({ user });
    } 
  });
```
When the user signs in, the `onAuthStateChanged` method checks the Firebase database to see if the user was already previously authenticated. If they were, we set the state with the user's details.

Now, we can update the UI to reflect that the user has been logged in! 

### Additional resources
[Firebase Authentication Documentation](https://firebase.google.com/docs/auth/web/password-auth)