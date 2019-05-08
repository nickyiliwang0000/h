<!-- Student takeaway: -->
<!--Student will be able to:
- Create an object literal
- Retreive the value on a property of an object using dot notation
- Retreive the value on a property of an object using bracket notation
- Update the value of a property using using dot notation
- Update the value of a property using using bracket notation
- Add a property to an object using dot notation
- Add a property to an object using bracket notation
- Write a for-in loop
 -->
# Objects
We learned [in a previous lesson](https://github.com/HackerYou/bootcamp-notes/blob/master/programming-fundamentals/intro-to-programming.md#data-types) that the data types of JavaScript values are: 

Data type | Description | Example
---|---|---
number | Integers & decimals/floats | `10`, `10.001`
string | Characters including spaces | `'internetUser993'` `"123 Main St."`
boolean | A reserved keyword that looks like an English word| `true`, `false`
undefined | Does not have a value | `undefined`
null | Has a value of nothing | `null`
object | A set of organized data | `{}`

> There's also a (new in ES6) data type called Symbol but it's used mostly in library creation and you won't see it much.

We've seen numbers, strings, booleans, and `undefined` when working with variables (these are sometimes known as [_primitives_](https://developer.mozilla.org/en-US/docs/Glossary/Primitive)). Now we're gonna talk about _objects_!

Objects are incredibly useful for storing paired and grouped data in JavaScript. You can think of them as containers. Inside the container are properties, which are composed of **key-value pairs**. Each property contains a name (i.e. a key) and a value which can be referenced directly. 

![Diagram of key value pairs as properties in an object](https://hychalknotes.s3.amazonaws.com/objects.png)

Another way to think about JavaScript objects is to compare them to real-life objects. An apple is an **object** and it has **properties** like colour, cultivar, sugar content, etc.

## Defining an object
The syntax for creating an object looks like this:

```js
const myObject = {
  propertyOneName: propertyOneValue,
  propertyTwoName: propertyOneValue,
  propertyThreeName: propertyOneValue,
};
```

In JavaScript, we might represent information about an apple in an object, like so:

```js
const apple = {
  colour: 'red',
  cultivar: 'Honeycrisp',
  sugarContent: 200
};
```

> Curly brackets with comma separated properties is the _object literal_ notation for making objects. There are other ways of making objects which will be covered [in other lessons](https://github.com/HackerYou/bootcamp-notes/blob/master/applied-javascript/class-based-programming.md).

### Object naming conventions
* Property names follow [the same rules](https://github.com/HackerYou/bootcamp-notes/blob/master/programming-fundamentals/variables.md#variable-naming-conventions) as variable names.
* Property names are always strings but the quotes are optional if the strings are valid variable names.
* The value of an object property can be any of the primitive types (number, string, boolean, null and undefined) or another object (creating a nested tree structure), you can also store functions on a property.
* In JSON, the last property is not followed by a comma.

## Accessing values in an object
There are two ways of accessing values in an object. One is called _dot notation_. It looks like this:

```js
myObject.propertyName;
```

The other is called _bracket notation_. It looks like this:
```js
myObject["propertyName"];
```
Note that in bracket notation, the property name is contained within quotation marks.

Most of the time you'll use dot notation, but bracket notation is useful if the property names require quotes **or** if they are unknown at runtime (e.g. the user's input is used to retrieve a property).

## Retrieving values from an object

Here is another example object: 
> Note that objects can be nested inside each other. 

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
  }
}
```

To get a property's value from an object you need to know the property name (e.g. `shoes`). 

dot notation | bracket notation
--- | --- 
`clothing.shoes` | `clothing['shoes']` 

## Updating values in an object

To update a property value you need to know the property name. Use the assignment operator (`=`) to assign a value to the property name.

dot notation | bracket notation 
--- | --- 
`clothing.shoes = 4` | `clothing['shoes'] = 4`

## Adding properties to an object
To add a new property to an existing object, define a new property and value on that object.

dot notation | bracket notation 
--- | --- 
`clothing.scarves = "too many!"` | `clothing['scarves'] = "too many!"` 
`clothing.uglyClothes = null` | `clothing['uglyClothes'] = null` 

Note that if you have a variable in your code, you may add it as a key in an object using bracket notation:
```js
let newItem = "dresses"

clothing[newItem] =  2;
console.log(`I have ${clothing.dress} dresses.`)
// I have 2 dresses.
```
The line that adds the property to the object remains the same no matter what the new item is, and **even if** we don't know what the new item is yet.

> You may be wondering: can I store a function to an object? Yes! This what's called a _method_ and we'll cover them in detail [in another lesson](https://github.com/HackerYou/bootcamp-notes/blob/master/programming-fundamentals/arrays-and-methods.md).

## Exercises

Download [this file](https://hychalknotes.s3.amazonaws.com/object-exercise-bootcamp.zip) and complete the exercises within.

## Iterating through an object

A _for-in loop_ can be used to iterate over the properties of an object and execute a block of statements.

The syntax looks like this:

```js
for (let variable in object) {
  //statements
}
```

**Note**: 

* The property name is assigned to the `variable` on each iteration. This `variable` can be called anything you want, a common name might be something like `key`, since the value it gets is the name of the key from the property.
* There is **no guarantee that the properties are retrieved in the same order they were inserted**. Browsers will often keep the order the same but it's just not guaranteed.

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

Here we use bracket notations to access the properties stored in the object. For example the first pass of the `for-in` loop sets the `item` variable to have the value of `"socks"`. So when we say `clothing[item]` what the browser really sees is `clothing["socks"]`. And each iteration changes the value of `item`.

The output looks something like this:

```js
I have 34 socks
I have 2 shoes
I have 3 pants
```

## Exercises
Download and complete [these exercises](https://hychalknotes.s3.amazonaws.com/object-iteration-exercises-bootcamp.zip) about iterating over an object.



