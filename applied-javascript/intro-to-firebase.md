
<!-- Student takeaway -->
<!-- By the end of this lesson, the student should know:
- 
-->
# Intro to Firebase
## A bit of web app history
One hundred million years ago, web development was divided into two camps: front-end and back-end.

**Front-end** development is concerned with the look, feel, and design of a site. The front-end, or _client side_, is where the user interacts with the application.

**Back-end** development focuses on data retrieval and storage. Getting data from a database to the browser so the front end has something to show. It is sometimes referred to as the _server side_ of your application. 

All of the applications that we've built up until this point are front-end applications: they are not hooked up to any kind of database, and since we don't know any back-end languages like PHP or server-side JavaScript environments like Node.js, we haven't been able to build or or manage our own databases.

Until now!

## Firebase
Firebase is a web application maintained by Google that allows us to use client-side JavaScript to create and store information inside a database.

It does this by providing us with a web API with which to interact in much the same way that we have been interacting with APIs. Firebase also makes other traditionally challenging back-end tasks, like setting up user authentication for our websites using a third party, accessible to JavaScript developers. 

### Setting up a Firebase project
Navigate to <https://firebase.google.com/> and click 'GET STARTED'.

> Firebase was acquired by Google in 2004, so you'll need to pick one of your Google accounts to log in.

Once you've logged in, you should see a screen that looks like this:
![Welcome screen from Firebase](https://hychalknotes.s3.amazonaws.com/firebase-set-up-step-1.png)

1. Click 'Add Project'
![Step 2](https://hychalknotes.s3.amazonaws.com/firebase-set-up-step-2.png)

1. Give your project a name. Let's call ours `first-firebase-app`. 
  * Choose whether to allow Google to capture data about your use of Firebase.

1. Press 'Continue' and 'Create project'

1. You'll now be at the Firebase dashboard. This is where you can manage all of your different database applications, set up new databases, and see what information is inside of them. We only have one right now (the one we just created), so we don't have to worry to much about this dashboard just yet.
![Step 3](https://hychalknotes.s3.amazonaws.com/firebase-set-up-step-3.png)
1. Click on the `</>` logo which leads to the Firebase configuration for web. This will cause a modal to pop up with an embed code. The code should look something like this:
  * ```javascript
  <script src="https://www.gstatic.com/firebasejs/3.6.5/firebase.js"></script>
  <script>
  var config = {
    apiKey: "AIzaSyAmSlZ6sNfNpj2QvvE_-fGWAFP9uQcRyGI",
    authDomain: "first-firebase-project-febc3.firebaseapp.com",
    databaseURL: "https://first-firebase-project-febc3.firebaseio.com",
    storageBucket: "first-firebase-project-febc3.appspot.com",
    messagingSenderId: "47212023087"
  };
  firebase.initializeApp(config);
  </script>
  ```

Make an HTML file and paste this script tag into it before the closing `</body>` tag.

Open the HTML document in your browser and type `firebase` into the console. You should see something like this:
`Object {__esModule: true, SDK_VERSION: "3.6.5", INTERNAL: Object, default: Object}`

If you see that, then Firebase has been initialized!

### Setting up a database

For now, we'll just be working with the database itself. 

1. Click on Develop' > 'Database' in the sidebar. 

#### DO NOT CHOOSE CLOUD FIRESTORE

2. Scroll down and choose 'Realtime Database'. 
3. Choose 'Create database'.

![create a database](https://hychalknotes.s3.amazonaws.com/firebase-create-database.png)

  * We're in development, so we want to choose 'Test mode' in order to allow anyone to read and write from the database. Later on, you might want to lock down the database so that only specific users or sites can access this database. 

4. Select 'Start in test mode' and press 'Enable'.
  * Make sure the dropdown menu next to the heading 'Database' has 'Realtime Database' selected.

![select realtime database](https://hychalknotes.s3.amazonaws.com/realtime-db.png)

5. Navigate to the `Rules` tab and check that `.read` and `.write` are set to `true`.
  * This alert is okay to dismiss - your data is not sensitive and no one else knows that your database even exists. Again, you can change this when you publish your final site.

## Data structure in Firebase

Data is organized a little bit differently in Firebase than in traditional relational databases written in _structured query language_ (SQL). There are no tables or records; everything is stored in a large JSON object with an associated key. 

## Adding data to our Firebase database
Right now, our database is empty. Let's put some stuff in it. 

### Where do we want to put our data?
Inside your `<script>` tags, write the following code: 

```javascript
const dbRef = firebase.database().ref();
```

We're creating a variable to hold a reference to an instance of our Firebase database, which lives at `firebase.database().ref`. This is where we want to get or send data.

We can pass an argument to Firebase's `ref` function to create a reference to a specific location in our database: 

```javascript
const users = firebase.database().ref('users');
```

A nested location reference would look like this:

```javascript
const singleUser = firebase.database().ref(`users/DoriArjan`);
```
> Try not to nest your data more than 3 layers deep. 

### Write methods in Firebase

The Firebase method `push()` creates a **new node** that is stored as the value for a Firebase-generated key. It returns an object with that key. 

```js
  dbRef.push('first push to Firebase');
// this is returned:
// e {repo: t, path: t, queryParams_: t, orderByCalled_: false, then: ƒ, …}
```

```bash
// The database is updated like this:
{
    -LYYnjbTOR0Qq03ehjb1: 'first push to Firebase'
}
```

> You'll most often use `.push()` when you are creating an instance of something that needs to be unique (e.g. a user ID, a session, an ordered list of tasks to complete).

The Firebase method `set()` is used to overwrite the data at a specific reference that you decide **and** for all its children.

This method returns a promise and takes a callback that will be called when the database has been updated. 

```js
const editorTheme = {editorTheme: 'Monokai Bright'};
let userId = `-LYYnjbTOR0Qq03ehjb1`;
const addToProfile = (profileData) => firebase.database().ref(`/${userId}`).set(profileData);
addToProfile(editorTheme);
```
```bash
// The database is updated like this:
{
  -LYYnjbTOR0Qq03ehjb1:{
    editorTheme:'Monokai Bright'
  }
}
```
Let's create an object with lots of information in it and push it to Firebase.
```js
const userSettings = {
  editorTheme: 'Monokai Bright',
  tabs:4,
  fontSize:20,
  paid:false
}
addToProfile(userSettings);
```

Change the tabs property and push again.

```js
userSettings.tabs = 2;
addToProfile(userSettings);
```
No problem! We're pushing a complete copy of the `userSettings` object with all properties intact. What happens if we don't want to write all the properties out, just add a couple?

```js
const moreUserSettings = {company:'HackerYou', coursesTaught:{fall:'bootcamp', winter:'bootcamp', spring:'bootcamp', summer:'partying'}};
addToProfile(moreUserSettings);
```
Oh no! We overwrite the child nodes if we don't include them in the object we're pushing to Firebase.

The Firebase method `update()` is used to write to specific nodes **without overwriting their what's already there**. 

```js
let newUserSettings = {company:'U of T'};
const changeSetting =(settingToChange) =>{
  firebase.database().ref('/-LYYnjbTOR0Qq03ehjb1').update(settingToChange);
};
```
```bash
// The database is updated like this:
{
  -LYYnjbTOR0Qq03ehjb1:{
    company:'U of T',
    coursesTaught:{fall:'bootcamp', winter:'bootcamp', spring:'bootcamp', summer:'partying'}
  }
}
```
> If a node doesn't exist when you try to update it, Firebase will create it.

## Grabbing data from Firebase
Now that we have some data stored in our database, let's retrieve it using the `.once()` method:

```javascript
const dbRef = firebase.database().ref();

dbRef.once('value', (data) => {
  console.log(data.val());
});

```
You will get back something that looks like this:

```js
{-LYYnjbTOR0Qq03ehjb1:{
  company:'U of T',
  coursesTaught:{
    fall:'bootcamp', 
    winter:'bootcamp', 
    spring:'bootcamp', 
    summer:'partying'}
  }
}
````

Let's break down what's happening here line by line:

```js
// Once again, we create a reference to our Firebase database.
const dbRef = firebase.database().ref();

// We call the `.once()` method here with the `value` argument 
// to ask for our Firebase database.
// We pass the return into our callback function using the `data` parameter.
dbRef.once('value', (data) => {
  //Using Firebase's .val() method, we get the content of our data
  // and log it to the console
  console.log(data.val());
});
```

## Listening for changes to data in Firebase
Usually you'll want to get data more than once -  especially if it's being updated elsewhere in the code or by multiple users. Remember `onClick` and `onChange` from jQuery? Firebase has its own built-in events we can use to update our app when new data has entered the database.

Let's say we're building a game and someone just hit a new high score - we want to make sure to listen to that score entering the database so we can update our Hall of Fame.

```javascript
const scoresRef = firebase.database().ref('scores/');

dbRef.on('value', (data) => {
  console.log(`New info coming in: ${data.val()}`);
  // code to update the Hall of Fame would go here
});
```

We can confirm that this is working by manually pushing a new entry into our database from the console: `dbRef.push('a new high score')`

## Data structure in Firebase
As your data gets more complex, you may want to start nesting your data in collections in order to help express relationships more clearly:

```javascript
{
  users:{
    0:{
      name:'Blair',
      hobbies: {
        0: 'skiing',
        1: 'rowing',
        2: 'running'
      }
    },
    1: {
      name:'Goresh',
      hobbies: {
        0: 'biking',
        1: 'guitar',
        2: 'running'
      }
    },
    2: {
      name:'Jean-Yves',
      hobbies: {
      0: 'collage',
      1: 'guitar',
      2: 'skiing'
      }
    }
  },
  peopleWhoLikeSkiing:{
    0: 'Blair',
    1: 'Jean-Yves'
  }
}
```

You **can** nest data real deep but **avoid more than three levels of nesting** whenever possible. When you fetch data from a location in the database, all of the child nodes come along with it. It's best practice to keep your data structure as flat as possible.

If this means your data is somewhat repetitive:
```javascript
{
  users:{
    0:{
      name:'Blair',
      hobbies: {
        0: 'skiing',
        1: 'rowing',
        2: 'running'
      }
    },
    1: {
      name:'Goresh',
      hobbies: {
        0: 'biking',
        1: 'guitar',
        2: 'running'
      }
    },
    2: {
      name:'Jean-Yves',
      hobbies: {
      0: 'collage',
      1: 'guitar',
      2: 'skiing'
      }
    }
  },
  peopleWhoLikeSkiing:{
    0: 'Blair',
    1: 'Jean-Yves'
  }
}
```

Here, we could get all the `users` and then map through each of their hobbies to figure out who likes skiing. A more efficient way to do this in Firebase is to have a node that contains the information you're going to want. 

```js
const skiPeople = firebase.database().ref('peopleWhoLikeSkiing');
```

Every single value in Firebase has a key because Firebase is JSON notation, which is like an object. You can assign your own keys or have Firebase generate keys for you depending on the write method (i.e. `push` creates a new Firebase key, `set` and `update` do not). We can use this key to retreive any value. 

> Note that we **should not store arrays in Firebase** because [the index number is not permanent](https://firebase.googleblog.com/2014/04/best-practices-arrays-in-firebase.html).


## Upgrading our jQuery app using Firebase!
Now that we've learned some of the fundamental principles of how data gets created and managed between our code and Firebase, let's make our to do app even more useful by adding Firebase!
