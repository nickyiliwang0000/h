<!-- Student takeaway: -->
<!-- At the end of this lesson, the student will be able to:
- Identify that JavaScript is both class- and object-based
- Explain that a class can create many instances of a similar object
- Understand that `extends` adds information to an existing Class
- Remember that a derived constructor must call super in order to access `this`
- Create their own Class and extend it
-->

# Class-based programming
JavaScript is an _object-oriented_ programming language which means that the language is based on the idea of objects. You've created plenty of objects so far; why are they so important to the language and to programming in general?

Let's imagine that you were building your own text-based game about raccoons in JavaScript. You want to have a player (think back to our `Warrior` object) with some health, the ability to move around, and the ability to attack. Based on all the [data types](https://github.com/HackerYou/bootcamp-notes/blob/master/programming-fundamentals/intro-to-programming.md#data-types) we've learned about so far, an object called `raccoon` would be the best way to contain all of this information.

So you start by creating a player object:

```javascript
const raccoon = {
  health: 100,
  location: {
    x: 0,
    y: 0
  },
  equipment: [],
  walk: function() {
    // ...code to make your player walk around
  },
  attack: function() {
    // ...code to make your player attack
  }
}
```

Perfect! You now have a `raccoon` object that attacks, walks, has equipment, and has health. But a `raccoon` with no adversaries will soon take over the city, so you build a human to protect Toronto's trash bins:

```javascript
const human = {
  health: 100,
  location: {
    x: 0,
    y: 0
  },
  equipment: [],
  walk: function() {
    // ...code to make the enemy walk around
  },
  attack: function() {
    // ...code to make the enemy attack
  }
}
```

Notice anything? The `raccoon` and `human` objects are the exact same! If you wanted this game to be two-player (two `raccoon` objects) and have a hundred different enemies (a hundred `human` objects), you can see how you could end up writing a ton of repetitive code that would be difficult to track.

Thankfully, JavaScript's got your back! We can take advantage of something called _prototypal inheritence_ to make our lives easier.

## Prototypal inheritance
Once we realize that we want our `raccoon` and `human` have all (or many) of the same properties, it's a sign that they can probably share a common ancestor. Just like a dog and a cat both have fur and legs and so can be classified as **animals**, our raccoon and human both have health, location, equipment, and mobility, and so could be classified as **characters**.

In much the same way that a child inherits characteristics from their parents (e.g. eye colour, hair colour, height), so too can objects inherit characteristics from their parent objects. In JavaScript, this shared parent object is called a **prototype**.

How do we create a prototype in JavaScript? Using something called a _class_:

```javascript
class Character {
  constructor() {
    this.equipment = [];
    this.health = 100;
    this.location = {
      x: 0,
      y: 0
    }
  }
  walk() {
    // ...code to make a character walk around
  }
  attack() {
    // ...code to make a character attack
  }
}
```

Note that there are no commas in between methods within the constructor - if you try to put one, you will get a syntax error!

Think of classes like the blueprint or mould or boilerplate for building out your various objects. In our example, the `Character` class is a blueprint for building players, enemies, basically anything in the game that has health, a location, can attack, walk, etc. You might have an `vehicle` prototype if you wanted to build out garbage trucks and bicycles.

Once we have created our classes, we create objects that inherit from that class using the `new` keyword, like this:

```javascript
const raccoon = new Character();
const human = new Character();

console.log(raccoon.health); // 100
console.log(human.health); // 100
```

Now we have a raccoon object and a player object that both have health, equipment, etc. which they have inherited from their class (`Character`) without having re-define any of their properties or methods.

You'll also notice if you change the `health` property of your player, it won't effect the enemy and vice versa!

> You'll notice that we use capital letters when naming our classes - this is a common convention and is a helpful signal to other developers using your code. When a new feature simplifies the syntax of something that previously existed in the language, it is sometimes referred to as **syntactic sugar**  because it "sweetens" the way that particular thing is written.

## Customizing our class instances
Right now, every new character we create in the game will have the same health. But what if we wanted our raccoon and our human to have different health?

We can refactor our `Character` constructor like this:
```javascript
class Character {
  constructor(health) {
    this.health = health;
  }
}
```

And when we create a new raccoon or human or any other character, we can pass in that new character's health like this:

```javascript
const raccoon = new Character(200);
const human = new Character(500);
const dog = new Character(100);

console.log(raccoon.health); // 200
console.log(human.health); // 500
console.log(dog.health); // 100
```

## Classes and extends
One major benefit that classes have over constructor functions is that they can be _extended_. What does this mean? Let's imagine for a second that in the game you're making, your raccoon can choose to be either a warrior, mage, or sandwich artist. Depending on which option they choose, the raccoon gains certain benefits.

Using the `extends` keyword, we can extend our `Character` class into a new `SandwichArtist` class, like this:

```javascript
class Character {
  constructor() {
    this.health = 100;
    this.location = {
      x: 0,
      y: 0
    }
  }
  walk() {
    // ...code to make a character walk around
  }
  attack() {
    // ...code to make a character attack
  }
}

class SandwichArtist extends Character {
  constructor() {
    this.health = 1000;
  }
  bake() {
    // ... code that gives our sandwich artist the ability to bake parmesan oregano bread
  }
}
```

By using `extends`, we can grab all of the properties and methods from our `Character` class, and layer new methods on top of it like a delicious sandwich. We can also modify existing properties (here we've given our `SandwichArtist` a health property of `1000`, since eating all those sandwiches makes them extra healthy).

Now if we want to create a new sandwich artist for our game (we shall call him `archibald`), we use our `new` keyword:

```javascript
  const archibald = new sandwichArtist();
```

Oh no! We get an error: `ReferenceError: must call super constructor before using [this] in SandwichArtist class constructor`. This is because `extends` does not provide us access to the `this` keyword right out of the box. We must include a special method called `super()` inside of our constructor. This command invokes something called the _super constructor_ (i.e. the constructor method on the parent class), and must be placed before any references to `this` inside the constructor:

```javascript
class sandwichArtist extends Character {
  constructor() {
    super();
    this.health = 200;
  }
  bake() {
    // ... code that gives our sandwich artist the ability to bake parmesan oregano bread
  }
}
const archibald = new sandwichArtist();
```

We have now created a new object called `archibald`, that has a `health` of `200` and a `bake` method which it has inherited from the `sandwichArtist` class, as well as the `location` property, `walk` and `attack` methods that it inherited from the `Character` class.

Class extends are an awesome way to build upon objects that already exist, and this will be particularly useful when we start working with React!

Let's do this as a group, and then you'll try it on your own:
* Think of something that could act as a good class (e.g. vehicle,)
* Think of some properties that class might have (e.g. wheels, color, doors, drive, seats)
* Create some objects that inherit from that class using the `new` keyword
* Mess around with those objects independently of one another and see what happens!

## Additional resources
* [Let's Learn ES6 - Classes](https://www.youtube.com/watch?v=EUtZRwA7Fqc) is a great overview of the difference between objects and classes and how they work.
* [Better JavaScript with ES6: A Deep Dive Into Class](https://scotch.io/tutorials/better-javascript-with-es6-pt-ii-a-deep-dive-into-classes) which explains some of the differences classes in JavaScript and other languages
