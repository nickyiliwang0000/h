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
Putting `+` between two selectors targets the second element **only when**  it appears in the markup directly after the first element. This can be handy when you are trying to pad text, but only when it comes after an image element.

```css
img + p{
  padding-right:10px;
}
```
This rule will target all images that come after paragraphs.

## Direct child selector
Putting `>` between two selectors targets the second element **only when**  it is a child of the first element. No other instances of that second element will be selected, nor will any other children of that parent.

```css
.parent > .child {
  font-size:20px;
}
```
This will target everything with a class of `child` inside the element with a class of `parent`.

## Following selector
Putting `~` between two selectors targets every instance of the second element that appears in the markup after the first element.

```css
img ~ p {
  color:red;
}
```

This will select every paragraph that appears in the markup after an image tag, regardless of whether it is directly after the image tag or a couple paragraphs down.

### Will the following selector work when the following element is nested inside of a sibling element?

No! The element must be a direct sibling to the following selector. If we have an element that fits the following selector rule, but it is a sibling's child, the styles will not be applied. 

<!-- Try it in [this CodePen]()! -->

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

##More pseudo selectors

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