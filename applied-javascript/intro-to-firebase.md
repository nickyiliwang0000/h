<!-- Student takeaway -->
<!-- By the end of this lesson, the student should know:
  - How to configure their projects to use Firebase
  - Set up Firebase's Realtime Database
  - How to create a reference to their database
  - What the .push(), .set() and .update() method do, and the differences between them
  - How to listen for changes made to their database and get information from their database
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

It does this by providing us with a web API, which we can interact with, in the same way that we have been interacting with other APIs. Firebase also makes other traditionally challenging back-end tasks, like setting up user authentication for our websites using a third party, accessible to JavaScript developers. 

Firebase also comes with loads of other amazing features, like helping us set up user authentication for our websites using E-mail or Twitter.

## Setting up Firebase
To set up Firebase, navigate to [https://firebase.google.com/](https://firebase.google.com/) and sign in.
Firebase was acquired by Google in 2004, so you'll need to pick one of your Google accounts to log in.

1. Once you've logged in, you should see a screen that looks like the photo below. Click on the 'Get Started' button.
![Step 1](https://hychalknotes.s3.amazonaws.com/firebase-step1-2019.png)  

2. Click 'Add Project'.
![Step 2](https://hychalknotes.s3.amazonaws.com/firebase-step2-2019.png)  

3. Give your project a name. Let's call ours `first-firebase-app`. If you would like, you can uncheck 'Use the default settings for sharing Google Analytics for Firebase data'. Click 'Continue'. You make be asked to 'Customize data sharing for your new project', you do not need to check any of the boxes. Click 'Create Project'.
![Step 3](https://hychalknotes.s3.amazonaws.com/firebase-step3-2019.png)  

4. You'll be redirected to the Firebase dashboard. This is where you can manage all of the firebase tools related to your project, including authentication, database, storage and hosting. Before implementing any of the features, we need do a bit of configuration. On the 'Project Overview' tab, click on the '</>' icon. 
![Step 4](https://hychalknotes.s3.amazonaws.com/firebase-step4-2019.png)  

5. Firebase will provide some code that will link our application with the Firebase project we have just created. If you make an `html` file, you can paste this code right into it before the closing `</body>` tags.
![Step 5](https://hychalknotes.s3.amazonaws.com/firebase-step5-2019.png)  

```javascript
<script src="https://www.gstatic.com/firebasejs/5.8.6/firebase.js"></script>
<script>
  // Initialize Firebase
  const config = {
    apiKey: "AIzaSyCIA9bxxwIgMijlvzKRcNkVVfYOIEWGoD0",
    authDomain: "first-firebase-app-bbf53.firebaseapp.com",
    databaseURL: "https://first-firebase-app-bbf53.firebaseio.com",
    projectId: "first-firebase-app-bbf53",
    storageBucket: "first-firebase-app-bbf53.appspot.com",
    messagingSenderId: "266243704518"
  };
  firebase.initializeApp(config);
</script>
```

Be sure to change `var` to `const` to keep things consistent with the rest of your application.

Open up your console and type `firebase`. You should see something like this:
`Object {__esModule: true, SDK_VERSION: "3.6.5", INTERNAL: Object, default: Object}`

If you see this, you have successfully configured your project to use Firebase.

#### Setting up a _Realtime Database_

1. Now that we have configured our application to use Firebase, we can take advantage of all the cool tools Firebase have created. For this lesson we will just focus on utilizing their Realtime Database. Click on 'Database' on the sidebar, be sure to scroll down past Cloud Firestore. You will find the option to create a Realtime Database below.
![Step 6](https://hychalknotes.s3.amazonaws.com/firebase-step6-2019.png)

2. Click 'Create Database'.  
![Step 7](https://hychalknotes.s3.amazonaws.com/firebase-step7-2019.png)

3. We're just in development, so we want to choose **test mode** in order to allow anyone to read and write from the database. Later on, you might want to lock down the database so that only specific users or sites can access our database. For now, select 'Start in test mode'. Click 'Enable'.
![Step 8](https://hychalknotes.s3.amazonaws.com/firebase-step8-2019.png)

4. If you were successful at creating a database, you would be redirected to a page that looks like the one below.
![Step 9](https://hychalknotes.s3.amazonaws.com/firebase-step9-2019.png)

## Understanding data structure in Firebase

Data is structured a little bit differently in Firebase when compared to more traditional, relational databases like `SQL`. There are no tables or records, everything is stored in a large `JSON` object with an associated key. 

## Best practices for structuring data

You can nest data 32 levels deep, but just like Sass - avoid unneeded nesting whenever possible. When you fetch data from a location in the database, all of the child nodes come along with it. It's best practice to keep your data structure as flat as possible. 


```javascript
myProject = {
  user: "Simon",
  hobbies: {
    1: "skiing",
    2: "rowing",
    3: "running"
  }
}
```

Every value in Firebase has a key that is attached to it. We can use this key in order to grab any value we desire. You can assign your own keys, or have Firebase generate these keys for you depending on what methods you choose. 

## Adding data to our Firebase database
Right now, our database is empty. Let's put some stuff in it. 

### Where do we want to put our data?
Inside your `<script>` tags and after your config code, write the following: 

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
const singleUser = firebase.database().ref(`users/${userId}`);
```
> Try not to nest your data more than 3 layers deep. 

## Frequently used write methods in Firebase

`push()` - this creates a new node that is stored at a Firebase-generated key. It returns an object with a `key` property that's value is the key that was just created. 

`set()` - this can be used to write data to a specific reference that you decide. This method returns a promise and also takes a callback that will be called when the database has been updated. 

`update()` - this method can be used when writing to specific nodes without overwriting their child nodes. 

Let's try a few of these out! 

### Write methods in Firebase

#### `push()`
The Firebase method `push()` creates a **new node** that is stored as the value for a Firebase-generated key.

```js
const firebaseObj = dbRef.push('first push to Firebase');

console.log(firebaseObj);
```

```bash
// The database is updated like this:
{
  -LYYnjbTOR0Qq03ehjb1: 'first push to Firebase'
}
```

In your console you should see the object that `push()` returns. Under prototype, you will see the Firebase key stored under the property name `key`. To store and access the Firebase key that was created along with the push, you can type the following:

```js
const firebaseKey = firebaseObj.key;
console.log(firebaseKey);
```

> You'll most often use `push()` when you are creating an instance of something that needs to be unique (e.g. a user ID, a session, an ordered list of tasks to complete).

#### `set()`
The Firebase method `set()` is used to overwrite the data at a specific reference that you decide **and** for all its children.

This method returns a promise and takes a callback that will be called when the database has been updated. 

```js
const editorTheme = {
  editorTheme: 'Monokai Bright'
};

const userId = `-LYYnjbTOR0Qq03ehjb1`;

const addToProfile = (profileData) => {
  return firebase.database().ref(`/${userId}`).set(profileData);
}

addToProfile(editorTheme);
```

Since there was no data stored at `-LYYnjbTOR0Qq03ehjb1`, it just added a node with the editorTheme object as its value.

```bash
// The database is updated like this:
{
  -LYYnjbTOR0Qq03ehjb1:{
    editorTheme:'Monokai Bright'
  }
}
```

Let's see what would happen if that node already existed. We're going to create another object with lots of information in it and use `set()` to replace the node we previously created with this new object:

```js
const userSettings = {
  editorTheme: 'Monokai Bright',
  tabs: 4,
  fontSize: 20,
  paid: false
}

addToProfile(userSettings);
```

Change the tabs property and call `addToProfile` again. Be sure to pass the updated userSettings object.

```js
userSettings.tabs = 2;

addToProfile(userSettings);
```
No problem! We're pushing a complete copy of the `userSettings` object with all properties intact. What happens if we don't want to write all the properties out, just add a couple?

```js
const moreUserSettings = {
  company:'HackerYou',
  coursesTaught: {
    fall:'bootcamp',
    winter:'bootcamp',
    spring:'bootcamp',
    summer:'partying',
  }
}
addToProfile(moreUserSettings);
```
Oh no! With `set()`, we overwrite the child nodes if we don't include them in the object we're pushing to Firebase.

#### `update()`
The Firebase method `update()` is used to write to specific nodes **without overwriting their what's already there**. 

```js
const newUserSettings = {
  company:'U of T',
};

const changeSetting = (settingToChange) => {
  firebase.database().ref('/-LYYnjbTOR0Qq03ehjb1').update(settingToChange);
};

changeSetting(newUserSettings);

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

### Data structure in Firebase
As your data gets more complex, you may want to start nesting your data in collections in order to help express relationships more clearly:

```javascript
{
  users: {
    userOne: {
      name: 'Rick Sanchez'
    },
    userTwo: {
      name: 'Morty Smith'
    },
    userThree: {
      name: 'Snowflake'
    }
  }
}
```

Firebase lets us express this relationship by passing in a path such as `/users` to our `ref` method. So if we want to start adding some user properties inside of a `user` collection, we can do that like this:

```javascript
const userCollection = firebase.database().ref('/users');

userCollection.push({name: 'Rick Sanchez'});
```

Now `userCollection` refers to our `users` collection, and calling `.push` on it will allow us to add new users to that specific collection!

## Grabbing data from Firebase
Now that we have some data stored in our database, let's retrieve it:

```javascript
// Once again, we grab a reference to our firebase database.
const dbRef = firebase.database().ref();

// We call the `on` method here to grab the value of our Firebase database.
// When it comes back, we store access it in our callback function via the parameter `data`.
dbRef.on('value', (data) => {
  // We call `.val()` on our data to get the contents of our data to print out in the form of an object
  console.log(data.val());
});

```
You will get back something that looks like this:

`Object {-KaeZ7AVTJqwqItpFzLz: "hello!"}` - this is your database object!


## Listening for changes to data in Firebase
Remember `on()` from jQuery? Firebase has its own built in `on()` method, that we can use to listen for events. For example, we can listen for when any changes have been made to the database.

Let's say we're building a game and someone just hit a new high score - we want to make sure to listen to that score entering the database so we can update our high score table.

```javascript
const dbRef = firebase.database().ref();

dbRef.on('value', (data) => {
  console.log('New info coming in: ');
  console.log(data.val());
  // code to update the high score table here
});
```

We can confirm that this is working by manually pushing a new entry into our database from the console: `dbRef.push('pizza')`

## Code-along: Upgrading our jQuery app using Firebase!
Now that we've learned how data gets created and managed between our code and Firebase, let's power up our to-do app by adding in Firebase!

Download [to-do-app-firebase-start.html](https://hychalknotes.s3.amazonaws.com/to-do-app-firebase-start.html) and follow along.

### Create a Firebase project
Let's create a new Firebase project! Steps can be found above under 'Setting up Firebase'. Add the Firebase CDN to your `html` file and paste your config code above your document ready. 

```html
<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.1/jquery.min.js"></script>
<script src="https://www.gstatic.com/firebasejs/5.8.3/firebase.js"></script>

<script>
const config = {
  apiKey: "AIzaSyAFUEcWuGkredZ5AdxtSpcMWS1nvdXDCAc",
  authDomain: "to-do-app-example-ca27f.firebaseapp.com",
  databaseURL: "https://to-do-app-example-ca27f.firebaseio.com",
  projectId: "to-do-app-example-ca27f",
  storageBucket: "to-do-app-example-ca27f.appspot.com",
  messagingSenderId: "403656512635"
};
firebase.initializeApp(config);

$(document).ready(function(){
  ...
});
</script>
```

### Create a database
In order for us to store our to-do information, we will need to create a Realtime Database for this project. Steps can be found above under 'Setting up a _Realtime Database_'.

Once we've created a database, we will need to create a reference to our database in our application. Let's store our database reference in a variable at the top of our document ready.

```js
$(document).ready(function(){
  const dbRef = firebase.database().ref();
  ...
});
```

Our database needs to know about any new to-do items. When a user submits a new to-do, instead of just appending it on the page, we will want to push it to Firebase. In addition to the description of the to-do, we also need to keep track the completion status of each to-do. For every to-do item, let's organize the data into an object before pushing it to Firebase. 

```js
$('form').on('submit', function(e) {
  e.preventDefault();

  if ($('input').val() !== '') {
    // store what the user typed in a variable
    const toDoItem = $('input').val();
    
    //create todo object, set complete to false by default
    const toDoObj = {
      description: toDoItem,
      complete: false
    }
    
    //push to firebase our new toDoObj.
    dbRef.push(toDoObj);
    
    // clear input
    $('input').val(''); 
  };
});

```

Next, we will want to display all the to-dos on our page. All of our to-dos will live in Firebase, so we will have to listen for whenever a new to-do is added and put it on the page. We're going to use Firebase's `on()` method to listen for any changes made to our database. `on()` takes two arguments - an event and a callback function. `value` is a Firebase event that reads and listens for changes in our database. The callback will be executed when the event happens.

```js
dbRef.on('value', (data) => {
  //an object that represents our data, gets passed into our callback function.
  //We're able to call val() on this Firebase object and get a snapshot of our database
  const toDoData = data.val();

  console.log(toDoData)
})

```

We eventually want to map over our data and render a `li` element on the page for each to-do. Unfortunately the `map()` method could only be called on arrays. Let's convert our data object into an array. We're going to use a `for` in loop to `push()` each to-do into an empty array.

```js
dbRef.on('value', (data) => {
  const toDoData = data.val();

  const arrayOfToDos = [];

  for(prop in toDoData) {
    arrayOfToDos.push(`<li><span class="fa fa-square-o"></span>${toDoData[prop].description}</li>`)
  }

})

```

Now that we have this array of `li` elements, we can replace the HTML contents of the `ul` element with this array.

```js
dbRef.on('value', (data) => {
  const toDoData = data.val();

  const arrayOfToDos = [];

  for(prop in toDoData) {
    arrayOfToDos.push(`<li><span class="fa fa-square-o"></span>${toDoData[prop].description}</li>`)
  }

  $('ul').html(arrayOfToDos);
})
```

### Bonus: implementing the checkbox
We can upgrade our to-do app with one more feature. Try getting the checkbox data to also persist using Firebase. If you get stuck, checkout out the the answer key provided. You can download [to-do-app-firebase-answer.zip](https://hychalknotes.s3.amazonaws.com/to-do-app-firebase-answer.zip) to see the final code-along with the checkbox implemented. If you wanted more guidance checkout the steps below.

Since the complete status of each to-do changes on the click of the `li` elements. We will want to put our code inside that click listener.

```js

$('ul').on('click', 'li', function() {
  // We'll put our code here
});

```

When the user clicks on the `li`, we need to identify the corresponding to-do node in Firebase in order to update it. Unfortunately, with the way we originally rendered the `li`, there is no way to identify which to-do belongs to which node. Since each node is assigned a unique Firebase key, we can add this piece of data to each `li` when we render it. Let's revisit how we rendered each li and ammend it slightly:

```js
dbRef.on('value', (data) => {
  const toDoData = data.val();

  const arrayOfToDos = [];

  for(prop in toDoData) {
    arrayOfToDos.push(`<li data-key=${prop}><span class="fa fa-square-o"></span>${toDoData[prop].description}</li>`)
  }
  
  $('ul').html(arrayOfToDos);
})

```

We're using the data attribute to store thea appropriate Firebase key in each `li`, so we can use it later for the checkbox feature. [For more information on the data attribute, check out MDN](https://developer.mozilla.org/en-US/docs/Learn/HTML/Howto/Use_data_attributes).  


Now that we have a way to identify each to-do, we can store key of the targeted `li` in a variable. We'll use this key to create a reference to the correct node in our database.

```js

$('ul').on('click', 'li', function() {
  const selectedKey = $(this).data('key');
  const toDoItemRef = firebase.database().ref(`/${selectedKey}`);
});

```

Since we have a way to point to the correct node, we can get a snapshot of that data and update that specific to-do object in our database. Since we only want to [read the data once](https://firebase.google.com/docs/database/web/read-and-write#read_data_once), use We're going to use Firebase's `once()` method. After capturing the correct to-do, we will use `update()` to change the complete status to be the opposite of what it is currently using the not operator.

```js

$('ul').on('click', 'li', function() {
  // stores the value of the data-key attribute in a variable. This value is the corresponding Firebase key
  const selectedKey = $(this).data('key');
  // creating a reference to the correct node using the previous variable
  const toDoItemRef = firebase.database().ref(`/${selectedKey}`);
  // getting snapshot of the appropriate node without listening for changes
  toDoItemRef.once('value', (data) => {
    // grab the data
    const targeted = data.val();
    // update the complete status of the correct to-do
    toDoItemRef.update({
      complete: !targeted.complete
    })
  })
});

```
> Sidenote: `on()` vs. `once()`. Why are we using `once()`? In situations where we want to only get a snapshot of the data and not listen for any changes, `once()` is a more appropriate method. If we were to use `on()` for this checkbox feature, we would get an infinite loop! YIKES! Since we would be calling `update()` inside of the `on()`, the update to the database would trigger the `on()`, which would trigger the `update()`, which would trigger `on()`...∞💥🚨. Fortunately, Firebase offers `once()` and it only triggers...once 🤭, which is exactly what we want in this case.  

We're almost there! Now we're going to conditionally render a filled in checkbox or an empty checkbox, based on its status Firebase. For this one we will have to revisit how we rendered those `li` elements again. Since the checkbox are a span, and the look of the checkboxes depend on what class we give the spans - we have to figure out which class to render based on the to-do status.

```js
dbRef.on('value', (data) => {
  const toDoData = data.val();

  const arrayOfToDos = [];

  for(prop in toDoData) {
    arrayOfToDos.push(`<li data-key=${prop}><span class="${toDoData[prop].complete ? `fa fa-check-square-o`: `fa fa-square-o`}"></span> ${toDoData[prop].description}</li>`)
  }

   $('ul').html(arrayOfToDos);
})
```

To conditionally render the appropriate class, we're using something called a _[ternary operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)_. If `toDoData[prop].complete` evaluates to `true`, the operator will return `fa fa-check-square-o` (the checked version), otherwise it will return `fa fa-square-o` (the unchecked version).  

The data for our to-do app now persists! If a user were to refresh the page, all the data remains on the page. WOOHOO! 💃!
