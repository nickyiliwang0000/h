## Objects

The **primitive types** of JavaScript values are *numbers*, *strings*, *boolean values* (true and false), *null* (haven't discussed this yet), *symbol* (new in ES6!) and *undefined*. All other values are something called **objects**.

We can think of objects as containers. Inside the container are **properties** , which are referred to as **key-value pairs**. Each property contains a *name* and *value* which can be referenced directly. This is similar to our CSS rules.

![image](https://hychalknotes.s3.amazonaws.com/objects.png)

Another way to think about JavaScript objects is to compare them to real-life objects. An apple is an object and it has properties like colour, size, sugar content, etc.

```js
const apple = {
	colour: 'Red',
	size: 'Small',
};
```

#### Syntax
The syntax for creating an object looks like this:

```js
const myObject = {
	propertyOneName: propertyOneValue,
	propertyTwoName: propertyOneValue,
	propertyThreeName: propertyOneValue,
};
```

The curly brackets with comma separated properties is the "**object literal**" notation for making objects. There are other ways of making objects which will be covered later.

You may remember a similar layout from your sublime text settings:

![](http://wes.io/U0dv/content)

**Note**:

* property names are always strings but the quotes are optional if the strings are valid variable names
* the value of an object property can be any of the primitive types (number, string, boolean, null and undefined) or another object (creating a nested tree structure), you can also store functions on a property. More on that later.
* in JSON, the last property is not followed by a comma.

Here is an example object. Note how objects can be nested inside each other. 

```js
const clothing = {
	belt: "can't remember",
	socks: 34,
	shoes: 2,
	pants: 3,
	hat: true,
	tShirts: {
		smallSize: 3,
		mediumSize: 4,
		largeSize: 2
	},
}
```

### Retrieving values
To get a property value from an object you need to know the property name. There are two ways to get the value.

**Dot-Notation**

The generic syntax looks like this:
```js
myObject.propertyName;
```

To retrieve the amount of shoes in our clothing object:

```js
clothing.shoes;
2
```

**Bracket-Notation**

The generic syntax looks like this: `myObject["propertyName"];` **Note that the property name is a string with quotes here.**

To retrieve the amount of shoes in our clothing object:

```js
clothing["shoes"];
2
```

Bracket-notation is used if the property names require quotes or if they are unknown at runtime (e.g. user's input is used to retrieve a property).

#### Updating Values

To update a property value you need to know the property name. And again there are two ways to do this.

**Dot-Notation**
Simply assign the value to `myObject.propertyName`, like this:

```js
myObject.propertyName = new_value;
```

For example, if we bought some new pants then we can update the value like this:

```js
clothing.pants = 4;
clothing.pants; // 4
```

**Bracket-Notation**

```js
myObject["propertyName"] = new_value;
```

The same example using bracket-notation looks like this:

```js
clothing["pants"] = 4;
clothing["pants"]; //4
```

To add a new property to an existing object, simply use those one of the above notations to define a new property and value. This will update your object with the new property and value.

```js
clothing.scarves = 5;
```

**Exercise 1**:

Create an object called "HackerYou" which contains information about the number of courses offered, age of the school, name of instructors, etc. (any information you want to store really…). 

**Exercise 2**:

Create an object called "student" which has the properties: `id`, `name`, `age`, `GPA`, and `highSchool`. Add some values to the object. Write an expression that retrieve says the following: `"The student Homer Simpson (ID: 1) is 15 years old. They have a GPA of 1.4 and are from Springfield High"`. Try it with dot notations and bracket notation.

## Enumeration

The **for-in loop** can be used to iterate over the properties of an object and execute a block of statements.

The syntax looks like this:

```js
for (variable in object) {
  //statements
}
```

**Note**: 

* The property name is assigned to the `variable` on each iteration. This `variable` can be called anything you want, a common name might be something like `key`, since the value it gets is the name of the key from the property.
* There is no guarantee that the properties are retrieved in the same order they were inserted -- don't count on the order to stay the same. Browsers will *usually* keep the order the same… *it's just not guaranteed*.

Here's an example:

```js
const clothing = {
	socks: 34,
	shoes: 2,
	pants: 3
}

for (let item in clothing) {
	console.log("I have " + clothing[item] + " " + item);
}
```

Here we use bracket notations to access the properties stored in the object. For example the first pass of the `for in` loop sets the `item` variable to have the value of `"socks"`. So when we say `clothing[item]` what the browser really sees is `clothing["socks"]`. And each iterations changes the value of `item`.

The output looks something like this:

```js
I have 34 socks
I have 2 shoes
I have 3 pants
```

**Exercises**:

The following object is used in the exercises:

```js
const inventory = {
	apples: 2,
	oranges: 3,
	bananas: 6,
	milk: 2
}
```

**Level 1**
Use the inventory object to print a string that looks like this: `"We have 2 apples, 3 oranges, 6 bananas, and 2 milk in stock."`

**Level 2**
Iterate over the inventory object and print a list of the items. The output should look like this:

```js
There are 2 apples.
There are 3 oranges.
There are 6 bananas.
There are 2 milk.
```

