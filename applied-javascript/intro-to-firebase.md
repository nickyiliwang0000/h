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

It does this by providing us with a web API with which to interact in much the same way that we have been interacting with APIs. Firebase also makes other traditionally challenging back-end tasks, like setting up user authentication for our websites using a third party, accessible to JavaScript developers. 

Firebase also comes with loads of other amazing features, like helping us set up user authentication for our websites using E-mail or Twitter.

## Setting up Firebase
To set up Firebase, navigate to [https://firebase.google.com/](https://firebase.google.com/) and sign in.
Firebase was acquired by Google in 2004, so you'll need to pick one of your Google accounts to log in.

1. Once you've logged in, you should see a screen that looks like the photo below. Click on the 'Get Started' button:
![Step 1](https://hychalknotes.s3.amazonaws.com/firebase-step1-2019.png)  

2. Click 'Add Project'
![Step 2](https://hychalknotes.s3.amazonaws.com/firebase-step2-2019.png)  

3. Give your project a name. Let's call ours `first-firebase-app`. If you would like, you can uncheck 'Use the default settings for sharing Google Analytics for Firebase data'. Click 'Continue'. You make be asked to 'Customize data sharing for your new project', you do not need to check any of the boxes. Click 'Create Project'
![Step 3](https://hychalknotes.s3.amazonaws.com/firebase-step3-2019.png)  

4. You'll be redirected to the Firebase dashboard. This is where you can manage all of the firebase tools related to your project, including authentication, database, storage and hosting. Before implementing any of the features, we need do a bit of configuration. On the 'Project Overview' tab, click on the '</>' icon: 
![Step 4](https://hychalknotes.s3.amazonaws.com/firebase-step4-2019.png)  

5. Firebase will provide some code that will link our application with the firebase project we have just created. If you make an `html` file, you can paste this code right into it before the closing `</body>` tags.

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

#### Setting up _Realtime Database_

1. Now that we have configured our application to use Firebase, we can take advantage of all the cool tools Firebase have created. For this lesson we will just focus on utilizing their Realtime Databas. Click on 'Database' on the sidebar, be sure to scroll down past Cloud Firestore. You will find the option to create a Realtime Database below.
![Step 6](https://hychalknotes.s3.amazonaws.com/firebase-step6-2019.png)

2. Click 'Create Database'.  
![Step 7](https://hychalknotes.s3.amazonaws.com/firebase-step7-2019.png)

3. We're just in development, so we want to choose **test mode** in order to allow anyone to read and write from the database. Later on, you might want to lock down the database so that only specific users or sites can access our database. For now, select 'Start in test mode'. Click 'Enable'.
![Step 8](https://hychalknotes.s3.amazonaws.com/firebase-step8-2019.png)

4. If you were successful at creating a database, you would be redirected to this page:
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

Every value in Firebase has a key that is attached to it. We can use this key in order to grab any value we desire. You can assign your own keys, or have firebase generate these keys for you depending on what methods you choose. 

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
const singleUser = firebase.database().ref(`users/${userId}`);
```
> Try not to nest your data more than 3 layers deep. 

## Frequently used write methods in Firebase

`push()` - this creates a new node that is stored at a firebase generated key. It returns an object with a `key` property that's value is the key that was just created. 

`set()` - this can be used to write data to a specific reference that you decide. This method returns a promise and also takes a callback that will be called when the database has been updated. 

`update()` - this method can be used when writing to specific nodes without overwriting their child nodes. 

Let's try a few of these out! 

### Write methods in Firebase

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

> You'll most often use `.push()` when you are creating an instance of something that needs to be unique (e.g. a user ID, a session, an ordered list of tasks to complete).

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

```bash
// The database is updated like this:
{
  -LYYnjbTOR0Qq03ehjb1:{
    editorTheme:'Monokai Bright'
  }
}
```
Let's create an object with lots of information in it and replace the node we previously created with this new object:
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
    summer:'partying'}
  };
}
addToProfile(moreUserSettings);
```
Oh no! We overwrite the child nodes if we don't include them in the object we're pushing to Firebase.

The Firebase method `update()` is used to write to specific nodes **without overwriting their what's already there**. 

```js
const newUserSettings = {company:'U of T'};

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

// We call the `on` method here to grab the value of our Firebase database. When it comes back, we store access it in our callback function via the parameter `data`.
dbRef.on('value', (data) => {
  // We call `.val()` on our data to get the contents of our data to print out in the form of an object
  console.log(data.val());
});

```
You will get back something that looks like this:

`Object {-KaeZ7AVTJqwqItpFzLz: "hello!"}` - this is your database object!


## Listening for changes to data in Firebase
Remember `.on()` from jQuery? Firebase has its own built in `.on()`, that we can use to listen for events, like when any changes have been made to the database.

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

## Upgrading our jQuery app using Firebase!
Now that we've learned some of the fundamental principles of how data gets created and managed between our code and Firebase, let's power up our todo app by adding in Firebase!
