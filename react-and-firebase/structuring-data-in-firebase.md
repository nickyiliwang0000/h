<!-- Student takeaway -->
<!-- By the end of this lesson, the student should know:
- That the data in Firebase looks like an object
- Two different methods to add data to the database (push and set)
- That push doesn't create a key, while set does
- It's okay to repeat data if it makes querying easier
-->
# Structuring data in Firebase
In Firebase, data is structured as a JSON tree.

JSON trees look very similar to a data type you're already familiar with from JavaScript: objects!

The [Firebase documentation](https://firebase.google.com/docs/database/web/structure-data) gives the following example to what a data structure might look like inside of Firebase:

```JSON
{
  "users": {
    "alovelace": {
      "name": "Ada Lovelace",
      "contacts": { "ghopper": true },
    },
    "ghopper": { ... },
    "eclarke": { ... }
  }
}
```

You'll notice that here we have a `users` key whose value is three objects: `alovelace`, `ghopper`, `eclarke`.

The value of `alovelace` is also an object:

```JSON
"alovelace": {
  "name": "Ada Lovelace",
  "contacts": { "ghopper": true },
},
```

...and so on down the line. This nesting of objects is how data gets stored inside of Firebase.

## Adding a user to our user tree
So what if we want to add a user to our user tree from inside our application? We know we can use the `push` method to add items to our database. We'll need to find a way to point to the specific place (the user table) that we want to put the data.

```javascript
const newUser = {
  "mcurie": {
    "name": "Marie Curie",
    "contacts": { "ghopper": true },
  }
};
```

For this, we can use the `firebase.database().ref()` method, like so:

```javascript
const userTable = firebase.database().ref('users');
userTable.push(newUser);
```

This will push the `newUser` in to the `users` table at a new key and with the `newUser` object as a value. This might be what you want; it will now look something like this:

```JSON
{
  "users": {
    "alovelace": {
      "name": "Ada Lovelace",
      "contacts": { "ghopper": true },
    },
    "ghopper": { ... },
    "eclarke": { ... },
    "-KzZJKgt128qc5XKet9I": {
         "mcurie": {
            "name": "Marie Curie",
            "contacts": { "ghopper": true },
        }
    }
  }
}
```

If you wanted a cleaner structure, we can get more specific about our reference.

```javascript
const userTable = firebase.database().ref('users/mcurie');
userTable.push({
     "name": "Marie Curie",
    "contacts": { "ghopper": true },
});
```
This will now put a `mcurie` key on our `users` table! But because we used `push` there is still something odd going on!

```JSON
{
  "users": {
    "alovelace": {
      "name": "Ada Lovelace",
      "contacts": { "ghopper": true },
    },
    "ghopper": { ... },
    "eclarke": { ... },
    "mcurie": {
         "-KzZJKgt128qc5XKet9I": {
            "name": "Marie Curie",
            "contacts": { "ghopper": true },
        }
    }
  }
}
```

The `push` method is used to pass multiple things to your database, so it needs to come up with unique keys every time. There is another method we could use that will be better for our purposes: `.set()`.

```javascript
const userTable = firebase.database().ref('users/mcurie');
userTable.set({
     "name": "Marie Curie",
    "contacts": { "ghopper": true },
});
```

The `.set()` method is used to add data directory to a resource, and not just push multiple values to it. 

## Best practices for structuring data in Firebase
We may have lots data to store in our database. That's great! But when we get around to querying the database, a nested structure like this one:
```JSON
{
  "users": {
    "alovelace": {
      "name": "Ada Lovelace",
      "contacts": { "ghopper": true },
    },
    "ghopper": { ... },
    "eclarke": { ... },
    "mcurie": {
            "name": "Marie Curie",
            "contacts": { "ghopper": true },
        }
    }
  }
}
```

...is tough to navigate if we want a list of, say, all the users who have `ghopper` in their contacts. Read more about the best way to structure data in Firebase [here](https://firebase.google.com/docs/database/web/structure-data#avoid_nesting_data) but the takeaway is that **it is okay to repeat data** if it means that your queries don't have to get and filter through giant objects to do their job.

```JSON
{
  "users": {
    "alovelace": {
      "name": "Ada Lovelace",
      "contacts": { "ghopper": true },
      "peopleWhoHaveThisPersonAsAContact": {
        "ghopper": true,
        "mcurie": true
      }
    },
    "ghopper": {
        "name": "Grace Hopper",
            "contacts": { "alovelace": true },
            "peopleWhoHaveThisPersonAsAContact":{
              "alovelace": true,
              "mcurie": true
            }
        }},
    "eclarke": { ... },
    "mcurie": {
            "name": "Marie Curie",
            "contacts": { "ghopper": true },
            "peopleWhoHaveThisPersonAsAContact":{
              "alovelace": true,
              "ghopper": true
            }
        }
    }
  }
}
```
