Wouldn't it be awesome if, when you refreshed your browser, your web app didn't reset itself back to square one? What about if users could log in to your app, and it showed them preferences based on the last time they used it?

This is the power that Firebase gives you by unlocking the power of back-end database.

## A Bit of History about Web Apps
Historically, web development has been divided into two camps: **front-end developers** (that's you!) and **back-end developers**.

**Front-end** developers are concerned with the look, feel, and design of a site. They are in charge with how we interact with an application, and what it looks like.

**Back-end** development, on the other hand, are more focused on the server side of your application. A big part of their job often involves helping to make sure that information can be stored and retrieved from your database.

All of the applications that we've built up until this point are strictly **front-end** applications - they are not hooked up to any kind of database, and since we don't know any back-end languages like PHP or server-side JS environments like NodeJS, we can't build or or manage our own back end.

Until now.

## Introducing Firebase
Firebase allows us to use front end, client-side JavaScript in order to create and store information inside of our own database.

It does this by providing us with a web API to interact with much in the same way that we interacted with our APIs during JavaScript week.

Firebase also comes with loads of other amazing features, like helping us set up user authentication for our websites using E-mail or Twitter.

## Setting Up Firebase
Getting started with Firebase is very easy. Simply navigate to [https://firebase.google.com/](https://firebase.google.com/) and click 'Get started for free'.
Firebase was acquired by Google in 2004, so you'll need to pick one of your Google accounts to log in.

Once you've logged in, you should see a screen that looks like this:
![Step 1](https://hychalknotes.s3.amazonaws.com/1.png)

1. Click 'Create New Project'
![Step 2](https://hychalknotes.s3.amazonaws.com/2.png)

2. Give your project a name. Let's call ours 'first-firebase-app'. Press Ok. You'll now be at the Firebase dashboard. This is where you can manage all of your different database applications, set up new databases, and see what information is inside of them. We only have one right now (the one we just created), so we don't have to worry to much about this dashboard just yet.
![Step 3](https://hychalknotes.s3.amazonaws.com/3.png)
3. Click on the </> logo which leads to the firebase configuration for web. This will cause a screen to pop up with an embed code. It should look something like this:
![Step 4](https://hychalknotes.s3.amazonaws.com/4.png)

If you make an `html` file, you can paste this code right into it before the closing `</body>` tags.


```javascript
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

Open up your console and type `firebase`. You should see something like this:
`Object {__esModule: true, SDK_VERSION: "3.6.5", INTERNAL: Object, default: Object}`

If you see that, then Firebase is set up!

## Setting up the Database

For now, we'll just be working with the database itself. Click on **database** in the sidbar. 

![create a database](https://hychalknotes.s3.amazonaws.com/firebase-create-database.png)

We're just in development, so we want to choose "test mode" in order to allow anyone to read and write from the database. Later on, you might want to lock down the database so that only specific users or sites can access our database. 

Select `start in test mode` and press `enable`.

We'll also want to select  `realtime database` from the drop down menu next to the `Database` heading. 

![select realtime database](https://hychalknotes.s3.amazonaws.com/realtime-db.png)


The last step is navigating to the `Rules` tab. Ensure that `.read` and `.write` are set to `true`.

## Understanding Data Structure in Firebase

Data is structured a little bit differently in Firebase when compared to more traditional, relational databases like `SQL`. There are no tables or records, everything is stored in a large `JSON` object with an associated key. 

## Best Practices for structuring data

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


## Adding Data to Firebase
Right now, our database is empty. 

That's because our database is currently empty - let's fill it up. Inside some `<script>` tags or in an external `scripts.js` file, write the following code: 

```javascript
const dbRef = firebase.database().ref();
```

In order to post to or retrieve data from firebase, you'll require an instance of the database, which we've added above. 

You can also create specific location references like this: 

```javascript
const users = firebase.database().ref('users');
```

If you're trying to access a nested location, you can do so like this:

```javascript
const singleUser = firebase.database().ref(`users/${userId}`);
```

## Frequently used write methods in Firebase

`push()` - this creates a new node that is stored at a firebase generated key. It returns an object with a `key` property that's value is the key that was just created. 

`set()` - this can be used to write data to a specific reference that you decide. This method returns a promise and also takes a callback that will be called when the database has been updated. 

`update()` - this method can be used when writing to specific nodes without overwriting their child nodes. 

Let's try a few of these out! 

### Data Structure in Firebase
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

## Grabbing Data from Firebase
Now that we have some data stored in our database, let's retrieve it:

```javascript
var dbRef = firebase.database().ref();

dbRef.on('value', (data) => {
  console.log(data.val());
});

```
You will get back something that looks like this:

`Object {-KaeZ7AVTJqwqItpFzLz: "hello!"}` - this is your database object!

Let's break down what's happening here line by line:

* **var dbRef = firebase.database().ref();** - Once again, we grab a reference to our firebase database.
* **dbRef.on('value', (data) => {** - We call the `on` method here to grab the value of our Firebase database. When it comes back, we store access it in our callback function via the parameter `data`.

* **console.log(data.val());** we call `.val()` on our data to get the contents of our data to print out in the form of an object

## Listening for Changes to Data in Firebase
Remember onClick and onChange from jQuery? Firebase has its own built in events we can use to update our app when new data has entered the database.

Let's say we're building a game and someone just hit a new high score - we want to make sure to listen to that score entering the database so we can update our high score table.

```javascript
var dbRef = firebase.database().ref();

dbRef.on('value', (data) => {
  console.log('New info coming in: ');
  console.log(data.val());
  // code to update the high score table here
});
```

We can confirm that this is working by manually pushing a new entry into our database from the console: `dbRef.push('pizza')`

## Upgrading our jQuery App using Firebase!
Now that we've learned some of the fundamental principles of how data gets created and managed between our code and Firebase, let's power up our todo app by adding in Firebase!
