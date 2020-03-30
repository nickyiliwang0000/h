# CSS Grid

CSS Grid is a relatively new layout system available to us. It is a two-dimensional grid-based system, meaning it can handle both columns and rows. It is not meant to replace flexbox, floats or positioning, but is simply one more tool in our tool box.


## Creating our grid

To begin, we'll need to set the display property of our parent element.

* `display: grid;` will give us a grid that is a block level grid

Setting our display property alone won't create a grid for us. We need to tell our grid how to lay out our columns (vertical) and rows (horizontal). To do this, we need to set up our `grid-template-columns` and `grid-template-rows` properties.


### `grid-template-columns` & `grid-template-rows`

These properties take a unit of measurement, sometimes referred to as a _track size_, for each row or column you want to have. We will separate each row or column size with a space only, no commas. 

To begin, let's download [gridStarter.zip](https://hychalknotes.s3.amazonaws.com/gridStarter.zip).

Add the following CSS to our stylesheet:

```css
.container {
  display: grid;
  grid-template-columns: 25% 50% 25%;
  grid-template-rows: 150px 300px;
}
```
Not only can we use both pixel values and percentages, but we also have another unit of measurement available. 

## Creating space between grid items

In order to create gaps (sometimes referred to as _gutters_) between columns and rows, there are two properties available: `grid-row-gap` and `grid-column-gap` which can be condensed into the shorthand `grid-gap`. When using the shorthand, the first value indicates `grid-row-gap` and the second value indicates `grid-column-gap`. If you provide one value only, it will apply to both. This property is set on the grid container, and will only give you extra space between grid areas, not on the outer edges.

```css
.container {
  grid-gap: <grid-row-gap> <grid-column-gap>;
}
```

These properties will accept fixed or flexible units which will accomodate whatever dimensions you set your columns and rows to **unless they are set using percentages**. When we use percentages, those units cannot be overwritten and can result in horizontal overflow. This is why the `fr` unit is so powerful in CSS Grid. 

Let's look at what happens when we add `grid-gap: 40px;` to our grid and switch the values for `grid-template-columns` to percentages:

```css
.container {
  display: grid;
  grid-template-columns: 25% 50% 25%;
  grid-template-rows: 150px 300px;
  grid-gap: 40px;
} 
```

### Introducing the `fr` unit

CSS Grid introduces a new unit of measurement called the `fr` unit, meaning **fraction of the free space in the grid container**. The `fr` value is determined after any non-flexible columns or rows are declared. Meaning if you have a five-column layout where two columns are set to `100px` each and the remaining columns are `1fr` each, the free space will be split up into three fractions and distributed evenly between the remaining columns. This is very similar to how the `flex-grow` and `flex-shrink` properties work.

Let's change our CSS to match the following:

```css
.container {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr;
  grid-template-rows: 150px 300px;
  grid-gap: 40px;
} 
```

What happens if we change the second column value to be `300px`? The `fr` units scale according to the free space available once the rest of the columns have been defined.

### Explicit and implicit rows and columns

What happens if we have more items in our grid than we expected? 

Let's comment-in our remaining 5 elements so we have 12 grid items, and a grid set up to accomodate two rows of three items per column (i.e. a 2x3 grid). What will happen to the three extra elements?

CSS Grids will automatically fit your new content in a new row. The size of the row will be determined by the content that falls to that new row. These new rows are called _implicit rows_. The rows we created initially are called _explicit rows_.

### `grid-auto-flow`

Notice how the extra grid items get put in a new **row**, not a new **column**? This is because the default value for the `grid-auto-flow` is `row`. We can adjust this by changing this property's value to `column`. 

* **row**: default value
* **column**: any implicit items will create new columns

Another value, `dense` attempts to fill in holes earlier in the grid.

> Using `grid-auto-flow: dense;` will change the order of your grid items, which may create accessibility challenges. If the order of your content matters to the user's understanding, don't this value. 

### `grid-auto-rows`

To control your implicit rows, you can use the `grid-auto-rows` property. It is possible to provide multiple values for multiple implicit rows. However, [Firefox does not currently support multiple values](https://caniuse.com/#search=grid), so wait until the support is more robust to use it in production.

```css
.container {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr;
  grid-template-rows: 150px 300px;
  grid-gap: 40px;
  grid-auto-rows: 100px;
}
```

With the above code, any implicit rows will be 100px tall.

### `grid-auto-columns`

This property controls the size of implicit columns when `grid-auto-flow` is set to `column`. It can be used the same way as `grid-auto-rows` property. [Firefox does not support multiple values for this property](https://caniuse.com/#search=grid), however other browsers do.

## Dev tools

Firefox has fantastic CSS Grid inspector tools! Let's dive into them.

When you inspect element on a grid container, you should be able to see a small grid icon next to the `display: grid` rule. If you click on that icon, you will enable the _grid tools_. 

![Inspector tools showing a grid icon next to the css rule display:grid](https://hychalknotes.s3.amazonaws.com/Screen%20Shot%202018-01-13%20at%204.19.56%20PM.png)

Click on the layout tab in your dev tools, and you will see 'Grid Display Settings' and a small map of your grid. You can hover over the map and see more information about the specific grid area you're hovering.

Here are some tips to help you read the grid tools:

* Edge of explicit grid: solid line

![A small solid line](https://hychalknotes.s3.amazonaws.com/explict-grid.png)

* Explicit grid inner lines (explicit row or column lines): dashed line 

![A small dashed line](https://hychalknotes.s3.amazonaws.com/explicit-grid-line.png)

* Implicit grid (implicit row or column): dotted line

![A small dotted line](https://hychalknotes.s3.amazonaws.com/implicit-grid-line.png)

* Grid gap: crosshair lines

![Two solid parallel lines with light dashed lines in cross-hatch](https://hychalknotes.s3.amazonaws.com/grid-gap.png)

To learn more about the inspector grid tools, [check out this link](https://projects.invisionapp.com/share/3X87NEBYH#/screens/179720294_Grid).

### Grid line numbers

![A screenshot of the grid tools in Firefox, showing the grid-gap, explicit columns, explicit and implicit rows.](https://hychalknotes.s3.amazonaws.com/gridTools.png)

Notice those numbers? Those are _grid line numbers_. For every column and row we create, we also create grid lines. They start on the top left outside edge of our grid and go to the bottom right outer edge. Explicit and implicit rows and columns get numbered.

## Grid Item Placement

### `grid-column-start` and `grid-column-end` / `grid-row-start` and `grid-row-end`

To place our child elements in specific grid locations, we can take advantage of grid line numbers and use the properties `grid-column-start`, `grid-column-end`, `grid-row-start`, and `grid-row-end`. We can apply these properties to any child of the grid container. The `-start` properties refer to the grid line where you want your element to start in the grid, and the `-end` properties refer to the grid line where you want element to end.

These grid placement properties can take a number of different values:

* **number** you can use grid line numbers (remember the outside edges are counted). If you use a negative number, you will count from the end of the _explicit_ grid.

```css
.gridItem1 {
  grid-row-start: 2;
  grid-row-end: 4;
}
```

* **span < number >** if you want your grid child to span across the included number of grid tracks. Can be declared in both `grid-row-start` and `grid-row-end`.

```css
.gridItem1 {
  grid-column-start: span 3;
}
```

* **auto** will default to the automatic span of one, can also be declared in both `grid-row-start` and `grid-row-end`.

```css
.gridItem1 {
  grid-row-start: auto;
}
```

* **custom grid line name** if you've named your grid lines in `grid-template-columns` and `grid-template-rows` then you can use the names here (see "[Additional learning topics](https://github.com/HackerYou/bootcamp-notes/blob/master/css/css-grids.md#additional-learning-topics)" below).
* **span < grid line name >** if you want your grid child to span until it hits the included named grid line (see "[Additional learning topics](https://github.com/HackerYou/bootcamp-notes/blob/master/css/css-grids.md#additional-learning-topics)" below).

### Overlapping with Grid
By default grid will shift content to avoid items overlapping. If an overlapping grid item is in your design, then every item in the grid will need to have an explicit `grid-column-start` and `grid-row-start` value.

### Shorthand placement

* **grid-column** is the shorthand property for `grid-column-start` and `grid-column-end`
* **grid-row** is the shorthand property for `grid-row-start` and `grid-row-end`

For both properties above, the first value will specify the starting placement, which can be any of the value types listed above. The second value will specify the end value. The first and second values are separated with a `/`. 

```css
.gridItem1 {
  grid-column: 1 / -1;
}
```

You can also use the `span` keyword in the shorthand:

```css
.gridItem1 {
  grid-column: 1 / span 3;
}
```

A **third** shorthand property is also available to use, and that is the `grid-area` property. The syntax for this property is as follows:

```css
.gridItem1 {
  grid-area: <grid-row-start> / <grid-column-start> / <grid-row-end> / <grid-column-end>;
}
```

## The `repeat` keyword

The `repeat` keyword is used inside of the value for `grid-template-columns` and `grid-template-rows` when we want to repeat the value for a number of rows or columns. The `repeat` keyword requires at least 2 values. It looks like this: 

The **first value** that `repeat` takes is either:
* a positive number, representing the number of columns or rows to create

OR

* a keyword 
  * **`auto-fill`** 
  * **`auto-fit`** 
(detailed explanation of both keywords coming up below)

The **second value** that `repeat` takes is the size of the columns or rows to be created. Most often you will see this size represented in pixels (e.g. `200px`) or `fr` units (e.g. `1fr`).

Here are some examples of `repeat` and what the long hand version of it would look like:

```css
/*  Three columns of 50px each */
grid-template-columns: repeat(3, 50px); 
/*  same as saying: */
grid-template-columns: 50px 50px 50px;

/*  Two rows of 1fr each */
grid-template-rows: repeat(2, 1fr);
/*  same as saying: */
grid-template-rows: 1fr 1fr;
```

We can also give `repeat` more than one value to repeat. Note that the values are only separated by a space. Let's look at an example:

```css
grid-template-columns: repeat(4, 1fr 2fr);
/* same as saying: */
grid-template-columns: 1fr 2fr 1fr 2fr 1fr 2fr 1fr 2fr;
```

## Exercise

Try this exercise: [grid-placement-exercise-start.html](https://hychalknotes.s3.amazonaws.com/grid-placement-exercise.html). The answer key is available [here](https://hychalknotes.s3.amazonaws.com/grid-placement-exercise-answer.html).


# Extra Resources

For a gameified version of CSS Grids, try [Grid Garden](https://cssgridgarden.com/).

