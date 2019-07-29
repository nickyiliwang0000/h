<!-- Student takeaway -->
<!-- By the end of this lesson, the student should know:
- Three different kinds of CSS selectors (type, class, descendant)
- How to target elements that share 2 or more classes
- How to declare the same rule for multiple selectors
- The basic concept of inheritance
- The basic concept of specificity
-->

# CSS selectors and the cascade

Learning how to change properties and values on existing pages is important but in your career as a developer, you'll often be styling from scratch.

It's important to understand each of the ways you can select elements. Remember that **selectors** are used to specify the elements on the page to which the styles will be applied. Writing powerful CSS requires understanding inheritance and keeping your work organized. It's good practice to identify common styles in your site and write selectors and declarations once rather than repeating the same rule for multiple selectors.

## CSS selectors

### Type selector

This is the most basic CSS selector and is used to match every instance of the selected element type on the page. This is very helpful when you are setting default styles for the website. Note that these styles are applied to **all** matches.

The selector for any element is just that element name without the opening and closing angle brackets (`<>`).

`<strong>...</strong>` &rarr; `strong { ... }`

`<div>..</div>` &rarr; `div { ... }`

`<blockquote>Some quote</blockquote>` &rarr;`blockquote { ... }`

### Class selector

Using an element selector is powerful, but what if we have some `h2` elements that will differ slightly from the main style? What if a few of them need to be a different size, font, or colour than the rest? We can select subsets of element types using the **class** and **id** attribute values.

Let's say we have three paragraphs, but we only want the middle one to have a yellow background. Our normal rule of `p { background:yellow; }` wouldn't work here because it would turn them all yellow.

```html
<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod</p>
<p>tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam</p>
<p>quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo</p>
```

#### Adding a class attribute

We need to add a class attribute to the element we want to choose.

```html
<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod</p>
<p class="special">tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam</p>
<p>quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo</p>
```

In our CSS, we can write a new selector. We use the `.` period to denote the class attribute.

```css
/* Turns any element with a class of special yellow */
.special {
  background: yellow;
}

/* Turns any paragraph with the class of special yellow */
p.special {
  background: yellow;
}
```

In general, it's best to start writing your CSS using less specific selectors, then progressively more specific as your design requires. In the first example, the class can be applied to any element (`<p>`, `<div>`, `<a>`, whatever). In the second rule, the `.special` class **has** to be applied specifically to a `<p>` tag in order for the style to appear. Decide how specific you need to be.

#### IDs in the wild

You may sometimes see elements with an ID instead of a class like this: `<p id="special">...</p>`. As you know, IDs work like classes, but they can **only be used once** per page. We won't be using IDs to target elements for styling in CSS. However, if you run into them in the wild, know that they are denoted by a hash `#` symbol in CSS instead of the period that classes take.

```css
/* Turns the element with the ID of special yellow */
#special {
  background: yellow;
}
```

Your classes (and IDs) can be anything you want, but choose names that describe what the style is being used for rather than simply describing how a section looks.

| class name       | better class name   |
| ---------------- | ------------------- |
| `.yellow`        | `.warning`          |
| `.first-section` | `.welcome-banner`   |
| `.blueBorder`    | `.accessibilityTip` |

The name cannot contain spaces. Use camel casing (myClassName), kabob casing (my-class-name) or underscores (my_class_name) to separate words. Pick one and be consistent.

### Descendant selectors

Another way to target elements is to use 'parent child' or, 'descendant' selectors.

It may not always be the best case for us to go through our code and add a special class to every single element we want to select. Sometimes it's just as easy to first select the parent and then narrow in on the children.

Let's say we have two lists on a page:

```html
<ul class="groceries">
  <li>Milk</li>
  <li>Eggs (on sale at <a href="#">No Frills</a>)</li>
  <li>Bread</li>
  <li>Red Bull (Please print this <a href="#">Coupon</a>)</li>
</ul>

<ul class="sports">
  <li>Soccer</li>
  <li>Basketball</li>
  <li>Hockey</li>
  <li>Irish Bog Snorkeling (read more <a href="#">here</a>)</li>
</ul>
```

We want to change the colour of the links only in the first list.

**We can't just use `a { }` because that will select every link on the page!**

So we use a parent child selector:

```css
.groceries a {
  color: green;
}
```

This parent/child selector selects only the `a` elements within the class of `groceries`.

There is no limit to the number of child selectors you can use, however, try and take the shortest route when creating parent/child selectors and try not to go more than three levels deep (like Inception!).

For this same example, we could have written `.groceries li a` which adds the step to make sure the `a` has a parent of `li`.

## Targeting multiple classes

You'll often see elements with multiple classes and want to select some of the elements based on more than one class. Take this markup:

```html
<ul class="pie">
  <li class="fruit cinnamon">Spartan Apple & Cinnamon</li>
  <li class="chocolate nuts">Chocolate Pecan with Ganache</li>
  <li class="fruit caramel">Apple Caramel Oat Crumble</li>
  <li class="pumpkin nuts">Pumpkin Pecan-Praline</li>
  <li class="cinnamon fruit">Spiced Apple Crisp</li>
  <li class="fruit caramel">Garden Gold Peach Caramel</li>
  <li class="chocolate nuts">Walnut Chocolate Chip Cookie</li>
  <li class="pumpkin nuts">Maple Walnut Pumpkin</li>
  <li class="cinnamon fruit">Spiced Anjou Pear</li>
</ul>
```

Let's select only the items that have the classes `fruit` **and** `caramel`.

When we select one class, we use a leading period. When we select multiple classes, we use a leading period for each class and **no space** between the class names we're selecting:

```css
.fruit.caramel {
  background: lightblue;
}
```

The order in which you provide the class names does not matter, the selector will apply to all elements that have the included class names.

## Declaring CSS rules for more than one selector

Imagine that three different classes share an identical style:

```css
.caramel {
  background: orange;
  text-transform: uppercase;
  letter-spacing: 0.6px;
  font-style: italic;
}

.pumpkin {
  background: orange;
  text-transform: uppercase;
  letter-spacing: 0.6px;
  font-style: italic;
  color: white;
}

.chocolate {
  background: orange;
  text-transform: uppercase;
  letter-spacing: 0.6px;
  font-style: italic;
  color: brown;
}
```

In the above example, we are repeating the same CSS declaration. To condense our CSS, how do we target more than one class or element type with one CSS declaration?

The humble comma `,`.

```css
.caramel,
.pumpkin,
.chocolate {
  background: orange;
  text-transform: uppercase;
  letter-spacing: 0.6px;
  font-style: italic;
}

.pumpkin {
  color: white;
}

.chocolate {
  color: brown;
}
```

## Inheritance

With CSS, you'll often want to apply styles to a nested block of elements (e.g. all the links and list items inside a `nav`, or all the elements inside `main` ). CSS uses _inheritance_ (also known as _the cascade_) to reduce the number of styles you have to write explicitly. Not all properties are inheritable, but most typographical ones are. So, if we have a section and we want **all** the text of **all** the elements inside to be grey we can use inheritance to our advantage:

```html
<section class="content-box">
  <h2>Section Title</h2>
  <p>Some text within the section</p>
</section>
```

```css
.content-box {
  color: grey;
}
```

Here, all of the child elements of `.content-box` will have the CSS rule `color:grey;` applied to them, even if the `body` has a different font color. You may have noticed that on many websites there are a bunch of styles applied to the `body` selector. Why?

**To take advantage of typographic inheritance!**

An expansion of the example above might be:

```css
body {
  color: black;
}

.content-box {
  color: grey;
}
```

Here, the rule `color: black;` will apply to every child of the `body` tag, except `.content-box` and its children, because the inheritance of rules is being overridden by the explicit redeclaration of color.

This should make everything on the page black, right?

```css
.content-box {
  color: grey;
}

body {
  color: black;
}
```

Nope! Why not?

## Specificity

Sometimes your styles won't apply the way you expect them to. Often, the reason for the disconnect is that your rule isn't sufficiently specific. The math for calculating specificity can be found [on the W3C's website](https://www.w3.org/TR/selectors-3/#specificity).

If we take the example from before:

```css
.content-box {
  color: grey;
}
body {
  color: black;
}
```

The rule for `body` is less specific than the rule for `.content-box`. So even though `.content-box` initally inherits its color from `body` because it is a child of `body`, the browser will show the text inside `.content-box` to be grey.

> This is why it's **best practice to write your selectors from most general to most specific**: so you don't have to worry as much about the combination of inheritance and specificity. If you're working on legacy code, lots of your CSS challenges will come from inheritance and specificity.

The W3 docs on specificity can get a little heady so to check your selectors or just play around, try this link [CSS specificity calculator](https://specificity.keegan.st/) or [the archived version](https://web.archive.org/web/20151225215633/https://specificity.keegan.st/).

## Exercises

Let's open up [css-selectors.zip](https://hychalknotes.s3.amazonaws.com/css-selectors-bootcamp.zip) in our text editor and browser to practice these selector rules!
