  <!-- Student takeaway -->
  <!-- By the end of this lesson, the student should:
  - Know what a pseudo-class is
  - Know four common pseudo-classes (:hover, :visited, :active, :focus)
  - Know four advanced pseudo-classes (:first-child, :last-child, :nth-child, :nth-of-type)
  -->

# CSS pseudo-selectors

Each element present on a page has several states that can be associated with it. These states are often when an interaction like a hover or selection has taken place. To target these states with CSS, we need to write selectors.  These state-specific selectors are called _pseudo-classes_.
Pseudo-classes are appended right after the main selector with a colon, `:`. The four most common ones are:

* `:hover`: used to style an element when the user's cursor hovers over it. Often used on links, but can be applied to any element.
  ```css
  a:hover {
    color: red;
  } /* Change links to red when hovered */
  ```

* `:visited`: used to style a link that the user has already visited.
  ```css
  a:visited {
    color: yellow;
  } /* Change links to yellow when visited */
  ```

* `:active`: used to style an element when the user clicks the element.
  ```css
  input.email:active {
      background-color: pink;
  } /* turn pink when the user is actively engaged with the input (a.k.a. clicking on it) */
  ```

* `:focus`: used to style an element when it is in focus. Often used in form elements.
  ```css
  input.email:focus {
    padding: 5px;
  } /* add padding to the input box when it's being focused */
  ```
Check out the differences in [this CodePen](https://codepen.io/zkdan/pen/zMomOZ).
> By default, browsers outline certain elements when they are focused. There is a trend for people to remove this outline if it does not match the style of your site. This is bad for accessibility! The outline is there so that people navigating the page with a keyboard can see where the focus is. If you must remove the browser's default outline, **make sure you apply your `:hover` styles to `:focus` as well.**


## Advanced pseudo-classes
### `:first-child`
The `:first-child` selector targets the first child element of a specified parent.

```css
section p:first-child {
  color: red;
}
```
```html
<section>
  <!-- This one will be red! --><p>This is the first sentence</p>
  <p>This is the second sentence</p>
  <p>This is the third sentence</p>
  <p>This is the fourth sentence</p>
</section>
```

### `:last-child`
The `:last-child` selector performs the opposite task. It selects the last element of a specified parent.

```css
section p:last-child {
  color: red;
}
```
```html
<section>
  <p>This is the first sentence</p>
  <p>This is the second sentence</p>
  <p>This is the third sentence</p>
  <!-- This one will be red! --><p>This is the fourth sentence</p>
</section>
```

### `:nth-child`
The `:nth-child` selector allows you to provide arguments to target a specific child element within a parent element.
```css
section p:nth-child(3) {
  color:red;
}
```
```html
<section>
  <p>This is the first sentence</p>
  <p>This is the second sentence</p>
  <!-- This one will be red! --><p>This is the third sentence</p>
  <p>This is the fourth sentence</p>
</section>
```
Follow along in [this CodePen](https://codepen.io/zkdan/pen/VVmGMz) to see these values in action. 

The argument can be a number, like in the above example. It can also be the keyword `even` or `odd`, which will target all the even- or odd-numbered children of that parent, respectively.

To select each element at an interval of your choosing, provide that interval as an argument to the `:nth-child` rule. For example, to select every fourth element, we'd write:

```css
ul li:nth-child(4n) {
  background: blue;
}
```

To view more advanced arguments available to `:nth-child` and further pseudo-classes, visit [the docs](https://developer.mozilla.org/en-US/docs/Web/CSS/:nth-child) or play around with [http://nth-test.com/](http://nth-test.com/).  

CSS Tricks also has [a great article on useful `:nth-child` recipes](https://css-tricks.com/useful-nth-child-recipies/).

### `:nth-of-type`

If we wanted to select the first `p` tag from the markup below, how would we do it?

```html
<section>
  <h3>This is the title</h3>
  <p>This is the first sentence</p>
  <p>This is the second sentence</p>
</section>
```
Your instinct might be to use `:first-child`, like so:
```css
section p:first-child {
  background-color: red;
}
```
This selector is looking inside of `section` for the first child and it expects that first child to be a `p`. Because the first child is **not** a `p`, the selector bails out and no styles are applied.

This is where `:nth-of-type` comes in handy, as it's more specific. Let's try again using `:nth-of-type`.

```html
<section>
  <h3>This is the title</h3>
  <p>This is the first sentence</p>
  <p>This is the second sentence</p>
</section>
```

```css
section p:nth-of-type(1) {
  background-color: red;
}
```
Check out [this CodePen](https://codepen.io/zkdan/pen/ZmBMmb) to see if that worked.

## Selector exercises
In order to get amazing with CSS, you need selector chops! The only way to get good at writing selectors is to practice.

Since we aren't familiar with all of the available styles, they've been included for you, you just need to write the selectors.

Download the [css-selector-exercises.zip](https://hychalknotes.s3.amazonaws.com/css-selector-exercises.zip) and open the starter file in your browser. Replace `____` with your own selectors. You'll need to study the markup for a bit before. If you get stuck feel free to reference the notes, ask an instructor, or one of your fellow students.

There is also a `css-selector-exercise-ANSWER.html` provided, open it in your browser to view what the final product should look like.

![Final product](https://hychalknotes.s3.amazonaws.com/CSS-exercise.png)

Once you've got a good handle on CSS selectors, open up [css-challenge-selectors.html](https://hychalknotes.s3.amazonaws.com/css-challenge-selectors.html) and see if you can write some complete CSS rules of your own. 

The full answers and a reference of what your version should be like is [here](https://hychalknotes.s3.amazonaws.com/css-challenge-selectors-ANSWER.html).


