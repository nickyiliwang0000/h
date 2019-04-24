## BEM

One of the hardest parts of writing maintainable HTML/CSS is figuring out what to name our classes. The more elements we have on the page, the more class names we need to write, and the harder it is to keep track of what each one is responsible for. You can end up with what is sometimes called 'spaghetti code' - a mess of unreadable HTML/CSS that is very hard to update, let alone understand!

If only there were some kind of system that helping organize your classes so that they could remain easy to read, even as your project grows....

Enter **naming conventions**!

What is a naming convention? Well, it's a system of rules that helps us to determine how we should name something - in this case, how we should name our CSS classes. Using a naming convention is incredibly beneficial because it makes our code (and anyone else who is looking at our code and understands our naming convention) much more readable and easier to understand and use.

Naming conventions also help you think about your code in a more structured and organized way, which will lead to you writing more structured and organized code.

One particular naming convention that has seen a distinct rise of popularity over the past few years is called **BEM**, and this is the one we will look at today. 

### What is BEM?
BEM is an acronym that stands for **Block**, **Element**, **Modifier**. It is a system for breaking down the elements on your page (we'll call them 'components' from now on, since the E in BEM stands for Elements, and I don't want to confuse these two things) into discrete chunks that are easier to manage and reason about.

It does this by applying a naming convention that is universal and descriptive.

Before we dive to deeply into it, let's take a look at what BEM looks like in the wild:
```html
<ul class='nav'>
   <li class='nav__link'>Home</li>
   <li class='nav__link nav__link--active'>About</li>
   <li class='nav__link'>Portfolio</li>
   <li class='nav__link'>Contact</li>
</ul>
```

This would generate a 'nav' block with four 'link' elements, one of which represents the page the user is currently on and so has an additional modifier of 'active'.

So to break down the syntax of BEM, it looks like this:

```css
.block__element--modifier
```

### Is BEM a Part of CSS?
No - it's just a naming **convention** created by a group of developers at [Yandex](https://yandex.com/), basically Russian Google. Your code won't break if you don't use BEM, or use BEM incorrectly. It's just a system for helping you make sense of the relationship between your HTML and CSS.

### What is a component?
A component is a stand alone part of something bigger, like an application. If your website is a puzzle, then your components are your individual puzzle pieces. If it's a bike, then the wheels and gears and handlebars are all components.

Understanding what a component is is a crucial step in building modular and scalable websites. By breaking up the elements of our webpage into components, we can begin to compose and recompose them in different shapes in order to create a structure that is at once solid as well as malleable.

Some examples of components on a webpage would be a navigation bar, a header, a footer, a gallery, a hero image, a modal, a slide in menu.

Once we have determined what our components are, BEM can help us write classes that style these isolated sections.

## The Block
Let's start with the B in BEM, the block.

First of all, a block is always the highest level of any individual component. It's written with no additional syntax, like this:
```html
<div class='gallery'>
</div>
``` 

Some characteristics of blocks:
  - Blocks' names should describe their purpose (e.g. `task-card`, `user-profile`, `sidebar`)
  - Blocks shouldn't influence their environment other than to take up the space they are allotted

A note about blocks: 
- Blocks can exist inside other blocks (e.g. a `blog-entry` block could contain an `author-information` block that appears elsewhere on the site)

## The Element
Next up is the element. The element is a composite piece of a block that would never be used separately. A link inside your nav, for example, would never be used outside of the nav container. A single cell in a gallery slider would also never exist outside of the gallery.

Elements are always prefixed by the name of the block they come from and two underscores, like this:
```html
<div class='gallery'>
   <div class='gallery__cell'>
     <img src='....'>
   </div>
</div>
```

When naming elements, their name should always describe **what it is**, not **what it looks like**. 

Some notes about elements:
  - Not all blocks have elements.
  - All elements MUST live inside blocks. You cannot have an element that is outside of a block.

## The Modifier
The modifier is the last piece of the puzzle with BEM. It defines the appearance, state or behaviour of a block element. If we go back to our nav for a second:
```html
<ul class='nav'>
   <li class='nav__link'>Home</li>
   <li class='nav__link nav__link--active'>About</li>
   <li class='nav__link'>Portfolio</li>
   <li class='nav__link'>Contact</li>
</ul>
```

The modifier, `--active` is added to the element `nav__link` inside the `nav` block. We use the class `.nav__link--active` to style the active link so the user knows which page they are on. We'll look at some more examples of modifiers in the link below.

Some notes about modifiers:
  - Modifiers define appearance/state/behavior of a block OR an element
  - Modifiers define appearance (i.e. modifiers answer the questions "How big?"  "What color?" "Which theme?")
  - Examples: `btn--success`, `image--small`, `profile__headshot--blue-border`,`blog-post__heading--medium`,`blog--monokai`


### A simple button

Another classic example when it comes to learning BEM is a button:

```html
<a href="">
  <span>Buy Now!</span>
  <span>$20</span>
</a>
```

Here we have some markup, let's look at how we might use regular CSS classes here.

```html
<a href="" class="btn green">
  <span class="largeText">Buy Now!</span>
  <span class="largeText">$20</span>
</a>
```

With these classes in place, we might begin to style this button like this:

```css
.btn {...}
.green {...}
.largeText {...}

/*SCSS*/
.btn {
  .largeText{}
  .green{}
}
```

You will notice that with the plain CSS version, we don't have much organization. We have classes like `.green` and `.largeText` that could be used anywhere. But the problem with this that unless we start nesting, or getting very specific with the class names, they are not particularly closely related.

Let's now look at a BEM version.

```html
<a href="" class="btn btn--green">
  <span class="btn--large">Buy Now!</span>
  <span class="btn--large">$20</span>
</a>
```

Already you can see the classes start to make more sense on the HTML, and in our stylesheet, they really come together.

```css
.btn {...}
.btn--green {...}
.btn--large {...}
```

There is certain amount of explicitness in BEM which makes our code human-readable.

One of the key ideas of BEM is that you should be confident when you update your code.  If you change the `font-size` of `.btn--large`, you should be confident that you'll only be changing the large buttons' font. If you change the `font-size` of a selector like `.largeText`, you can't be sure of everywhere that change will take effect.

### Gotchas

#### Block or Element?
One gotcha that typically gets people, is: is this a block or an element?

- Is this code going to be reused AND it doesn't depend on other components?
  - If yes, you're looking at a block.
- Will this code __never__ exist outside the context of its parent element? 
  - If yes, you're looking at an element.

This tiny flowchart might help, too:
![flow chart for BEM clarification](https://hychalknotes.s3.amazonaws.com/BEM-flow-chart.png)

#### Specificity 
BEM won't prevent you from using excessive CSS specificity (ie `.nav .nav__listItem .btn--orange`), however it will help you start to identify areas that you can avoid this all together, and create cleaner more maintainable code.

#### Other Naming Conventions
There are lots of naming conventions out there, other systems you can look at include [SMACSS](https://smacss.com/) and [OOCSS](https://www.smashingmagazine.com/2011/12/an-introduction-to-object-oriented-css-oocss/). None of them are righter than any other ones, they're just different ways to do the same thing: keep your code organized and the developers who come after you sane.

##### Additional Resources:
- Additional Resources: Examples of BEM
- [BEM Methodology](https://en.bem.info/methodology/)
- [CSS Tricks on BEM](https://css-tricks.com/bem-101/)

