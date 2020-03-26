<!-- Student takeaway -->
<!-- By the end of this lesson, the student should know:
- How to use the following advanced CSS selectors:
    Adjacent (+)
    Direct child (>)
    Following (~)
    Attribute ([])
    Checked (:checked)
    Not (:not)
-->

# Advanced CSS selectors

By now, we have become pretty comfortable with the following selectors:

type | descendant | class name | id | group
---|---|---|---|---|
`p`| `ul li` | `.warning` | `#home` | `.warning, .success`

We're going to take a look at some more complex and specific selectors. 
Compatibility and examples of each can be found in this [excellent article](http://net.tutsplus.com/tutorials/html-css-techniques/the-30-css-selectors-you-must-memorize/).

>Remember that CSS is unidirectional (i.e. it only goes down): you can't select a parent if you only know the child, but you can select a child if you only know the parent. 

Download [adv-selector-playground.zip](https://hychalknotes.s3.amazonaws.com/adv-selector-playground.zip) for this lesson.

## Adjacent selectors
Putting `+` between two selectors targets the second element **only when**  it appears in the markup directly after the first element. For example, this can be useful when you want to add padding to any text on a page which comes directly after an image.

```css
img + p {
  padding-right: 10px;
}
```
This rule will target all paragraphs which come after images.

## Direct child selector
Putting `>` between two selectors targets the second element **only when**  it is a _direct child_ of the first element - that is to say, the second element is nested immediately inside the parent and not any more layers deep (as opposed to the more general parent-child selector). No other instances of that second element will be selected, nor will any other children of that parent.

Take a look at the following HTML:

```html
<div class="container">
  <article class="anElement">
    <h2>Lorem ipsum</h2>
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Illum, expedita?</p>

    <section class="anElement">
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quae, voluptatum.</p>
    </section>
  </article>
</div>

<aside class="anElement">
  <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Perspiciatis, earum.</p>
</aside>
```

We could write the following CSS:

```css
.container > .anElement {
  margin: 20px;
}
```
This will target everything with a class of `anElement` that is directly inside an element with a class of `container`. In our above HTML, that means we will be applying 20px of margin only to the `article` with a class of `anElement`, but not to the `section` or the `aside`.

## Following selector
Putting `~` between two selectors targets all instances of the second element which appear in the markup after the first element, and share the first element's parent. This is also called the _general sibling selector_.

```css
img ~ p {
  color:red;
}
```

This will select every paragraph that appears in the markup after an image tag, regardless of whether it is directly after the image tag or a couple paragraphs down.

Note that the following selector won't work if the element you're targeting is nested inside of a sibling element; it must be a direct sibling to the first element. If we have an element that fits the following selector rule, but it is a sibling's child, the styles will not be applied.

## Attribute selectors

Select elements with a specific attribute. We have done this with input types before, but it works with any type of attribute!

See these examples live [here](https://codepen.io/hackeryou/pen/VqGeRz).

### `a[href=" "]`
This selector finds all the links whose `href` values are **exactly** what's in the quotes and applies the specified styles.

### `a[href*=" "]`
This selector finds all the links whose `href` value **contains** what's in the quotes and applies the specified styles.

### `a[href^=" "]`
This selector finds all the links that **start with** what's in the quotes and applies the specified styles.

### `a[href$=" "]`
This selector finds all the links that **end with** what's in the quotes and applies the specified styles.

### `input[type='checkbox']:checked`

This selector finds all the checkboxes that **are** checked and applies the specified styles.

Kind of uninspired on it's own, but we can use this selector in conjunction with the sibling selector. 

Check out [this CodePen](https://codepen.io/hackeryou/pen/VqGKea) for an example.

## More pseudo selectors

### `:not()`

This selector finds all the elements except the one specified inside the smooth brackets and applies the specified styles.

Find an example [here](https://codepen.io/hackeryou/pen/maGrmw).

### `::first-letter`

This selector finds all the first letter of an element and applies the specified styles.

Find an example [here](https://codepen.io/hackeryou/pen/GPXjEv).

### `::first-line`

This selector finds the first line of every matched element and applies the specified styles.

When the size of the line changes because of a browser resize, the styles continue to apply only to the first line.

Find an example [here](https://codepen.io/hackeryou/pen/GPXjEv).

## Exercise

We can use CSS selectors to achieve some pretty powerful effects without any JavaScript.

Open up [3.23-advanced-css-selectors.zip](https://hychalknotes.s3.amazonaws.com/3.23-advanced-css-selectors.zip) to build a page with a toggle state.


## Resources
* See if you can finish everything in [the CSS Diner](https://flukeout.github.io/)! (This game's real favorite around here!)
* If you'd like another game, [here's one](http://toolness.github.io/css-selector-game)!