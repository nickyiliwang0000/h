You've probably heard that JavaScript is an 'object-oriented' programming language, and you've played around and created a lot of objects so far - but why are they so important to the language and to programming in general?

Well, let's imagine for a minute that you were building your own text based game in JavaScript. You want to have a Player (think back to our Warrior object) with some health, the ability to move around, and the ability to attack. Based on all the data types we've learned about so far (string, number, etc), an object seems like it would make the most sense for our Player to juggle all of these responsibilities.

So you start by creating a player object:

```javascript
const player = {
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

Perfect! You now have a player object that attacks, walks, has equipment, and health. But a player with no enemies is a pretty boring game, so you start to build an enemy object for your player to fight:

```javascript
const enemy = {
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

Notice anything? The enemy and the player objects are the exact same! Now imagine you had a two player game, and a hundred different enemies - you can see that you could end up writing a ton of repetitive code and it would become difficult to track very quickly.

Thankfully, JavaScript's got your back - we can take advantage of something called *prototypal inheritence* to make our lives much much easier.

## Prototypal Inheritance

Once we realize that we want our player and enemy have all (or many) of the same properties, it's a sign that they can probably share a common ancestor. Just like a dog and a cat both have fur and legs and so can be classified as *animals*, our enemy and player both have health, location, equipment, and mobility, and so could be classified as *characters*.

And much in the same way that a child inherits characteristics from their parents (eye colour, hair colour, height), so too can objects inherit characteristics from their parent objects. In JavaScript, this 'shared' parent object is called a *prototype*.

How do we create a prototype in JavaScript? Using something called a class:

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

Think of classes like the blueprint or mould (the technical term is a *prototype*) for building out your various objects. So in our example, the `Character` class is a blueprint for building players, enemies, basically anything that has health, a location, can attack, walk, etc. You might have an `animal` prototype if you wanted to build out dogs and cats.

Once we have created our classes, we create objects that inherit from that class super easily using the `new` keyword, like this:

```javascript
const player = new Character();
const enemy = new Character();

console.log(player.health); // 100
console.log(enemy.health); // 100
```

Now we have a player object and an enemy object that both have health, equipment, etc. which they have inherited from their class (Character) without having re-define any of their properties or methods.

You'll also notice if you change the `health` property of your player, it won't effect the enemy and vice versa!

(Small note: You'll notice that we use capital letters when naming our classes - this is a common convention and is a helpful signal to other developers using your code. When a new feature simplifies the syntax of something that previously exists in the language, you will often hear this called *syntactic sugar* - possibly because it sweetens the way that particular thing is written.)

## Customizing our Class Instances
Right now, every time we create a Person they will all have the same health. But what if we wanted our player and our enemy to have different health?

We can refactor our Character's constructor like this
```javascript
class Character {
  constructor(health) {
    this.health = health;
  }
}
```

And when we create a new monster or player, we can pass in the desired health that we want, like this:

```javascript
const player = new Character(200);
const enemy = new Character(500);

console.log(player.health); // 200
console.log(enemy.health); // 500
```



## Classes and Extends
One major benefit that classes have over constructor functions is that they can be *extended*. What does this mean? Well let's imagine for a second that in the game your making, your player can choose to be either a warrior, mage, or sandwich artist. Depending on which option they choose, the player gains certain benefits to their special abilities.

Well, using the `extends` keyword, we can `extends` our Character into a new Sandwich Artist class, like this:

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
    this.health = 200;
  }
  bake() {
    // ... code that gives our sandwich artist the ability to bake parmesan oregano bread
  }
}
```

By using `extends`, we can grab all of the properties and methods from our Character class, and layer on top of them new methods like a delicious sandwich. We can also modify existing properties (here we've given our `sandwichArtist` a health property of 200, since eating all those sandwiches makes them extra healthy)

Now if we want to create a new sandwich artist for our game (we shall call him 'Archibald'), we use our `new` keyword like before:

```javascript
  const archibald = new sandwichArtist();
```

Oh no! We get an error: `Uncaught ReferenceError: this is not defined`. This is because `extends` does not provide us access to the `this` keyword right out of the box. We must include a special keyword called `super()` inside of our constructor. This command invokes something called the *super constructor*, and must be placed before any references to `this` inside the constructor:

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

We have now created a new object called archibald, that has a `health` of 200 and a `bake` method which it has inherited from the sandwichArtist, as well as the `location` property, `walk` and `attack` methods that it inherited from the Person class.

Class extends are an awesome way to build upon objects that already exist, and we'll see why this is particularly useful when we start working with React!

Let's do this as a group, and then you'll try it on your own:
* Think of something that could act as a good class (a car, for example)
* Think of some properties that class might have (wheels, color, doors, drive)
* Create some objects that inherit from that class using the `new` keyword
* Mess around with those objects independently of one another and see what happens!

### Additional Resources
* [Let's Learn ES6 - Classes](https://www.youtube.com/watch?v=EUtZRwA7Fqc) is a great overview of the difference between objects and classes and how they work.
* [Better JavaScript with ES6: A Deep Dive Into Class](https://scotch.io/tutorials/better-javascript-with-es6-pt-ii-a-deep-dive-into-classes) which explains some of the differences classes in JavaScript and other languages
