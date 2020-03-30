## Advanced CSS Grids
### `auto-fit` and `auto-fill`

Repeat is super powerful when used with `auto-fit` and `auto-fill`. The difference between the two keywords is very subtle, but has to do with extra white space. Both fit as many rows/columns at a certain size as possible, while respecting grid gaps. At smaller breakpoints, the two act the same; it is only when we have extra whitespace available that we can see the difference.

* `auto-fill`: Fills the row with as many columns as it can fit at the specified size. New tracks can be empty, they will still take up the space allotted. 

* `auto-fit`: The browser will create as many tracks as it can at the specified size, but will collapse them if there are no extra elements to place.

Let's look at an example:

#### `auto-fill`
```css
.grid-container--fill {
  grid-template-columns: repeat(auto-fill, 100px);
}

```
![A screenshot illustrating the auto-fill keyword and how it maintains empty extra columns](https://hychalknotes.s3.amazonaws.com/Screen%20Shot%202018-05-27%20at%202.28.52%20PM.png)

Here, `auto-fill` is creating 11 tracks at the 100px size even though there is no content to fit inside the last three tracks. This can be handy when you need an element to be positioned in the last grid area in the explicit grid. If we were to add `grid-column-end: -1;` to the 7th item, it would live at the end of the row! 

#### `auto-fit`

```css
.grid-container--fit {
  grid-template-columns: repeat(auto-fit, 100px);
}
```

![A screenshot illustrating the auto-fit keyword and how it does not create extra columns](https://hychalknotes.s3.amazonaws.com/Screen%20Shot%202018-05-27%20at%202.29.04%20PM.png)

In the `auto-fit` example, our explicit grid ends after the 7th spot. We do see that the grid is creating 11 columns, but the 8th - 11th spots are collapsed. If we told our 7th item to end at -1 row, it would be in the exact same spot it is in now! 

### `minmax`

`minmax` is a method that takes two values, a minimum size, and a maximum size. It is used in the `grid-template-columns` and `grid-template-rows` properties.  

Let's adjust our CSS to the following:

```css
.container {
  grid-template-columns: 1fr minmax(400px, 1fr) 1fr;
}
```

Combining the `minmax` function with `auto-fit` and `repeat` can help create some intuitively responsive layouts. You can create a layout with a flexible number of columns as well as flexible widths of columns. Let's adjust our CSS to the following:

```css
.container {
  grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
}
```

A great resource for combining those properties is [this article by Rachel Andrew](https://rachelandrew.co.uk/archives/2016/04/12/flexible-sized-grids-with-auto-fill-and-minmax/), who is a member of the CSS Working Group. 

## `order`
`order` in grid is the same as `order` in flexbox. All grid items have a default of 0. Negative `order` values will make the grid item appear before the rest, a positive number will make the item appear after the rest. 

Using `order` on grid items will change the order of your grid items. If the order of your content matters to the users understanding then **do not use** this property. In general, would be fine for something like an image gallery but bad for blocks of text.

### Content sizing keywords
Instead of using a measurement unit or `fr` in our `grid-template-columns` or `grid-template-rows` we can also use content sizing keywords. Let's look at an example of these three keywords outside of grid before we see them in an example. 

#### `min-content`
`min-content` will make an element be the smallest width possible. This is usually dictated by the longest word.

<!-- <iframe height='265' scrolling='no' title='Content Sizing Keywords : min-content' src='//codepen.io/suzettemccanny/embed/jpwjoP/?height=265&theme-id=0&default-tab=html,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/suzettemccanny/pen/jpwjoP/'>Content Sizing Keywords : min-content</a> by Suzette McCanny (<a href='https://codepen.io/suzettemccanny'>@suzettemccanny</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe> -->

#### `max-content`
`max-content` will let an element be as wide as necessary to fit all of the content. In the case an element can be larger than it's parent, `max-content` will cause an overflow.

<!-- <iframe height='265' scrolling='no' title='Content Sizing Keywords : max-content' src='//codepen.io/suzettemccanny/embed/JBJgdL/?height=265&theme-id=0&default-tab=html,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/suzettemccanny/pen/JBJgdL/'>Content Sizing Keywords : max-content</a> by Suzette McCanny (<a href='https://codepen.io/suzettemccanny'>@suzettemccanny</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe> -->

#### `fit-content`
`fit-content` takes a value that will become the size of the element. Example: `grid-template-columns: fit-content(200px) 1fr 1fr;`

<!-- What's great about these keywords, is they are supported in all broswers that also support grids! Let's look at how we can use these in grids:

<iframe height='265' scrolling='no' title='Content Sizing Keywords - fit-content' src='//codepen.io/suzettemccanny/embed/GBMKvZ/?height=265&theme-id=0&default-tab=html,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/suzettemccanny/pen/GBMKvZ/'>Content Sizing Keywords - fit-content</a> by Suzette McCanny (<a href='https://codepen.io/suzettemccanny'>@suzettemccanny</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe> -->

### Grid alignment keywords
Unlike flexbox, the keywords to organize space on a grid do not change. `justify` will always refer to the row axis, and `align` will always refer to the column axis.

**justify** refers to space on the **row axis**


![A grid layout where the word 'row' is centered in the column](https://hychalknotes.s3.amazonaws.com/justify-row-axis.png)


**align** refers to space on the **column axis.**


![A grid layout where the word column is aligned to the bottom of each row](https://hychalknotes.s3.amazonaws.com/align-column-axis.png)

 
### Organizing space **within** the grid 

#### `justify-items` and `align-items`
The `justify-items` and `align-items` properties are set on the grid parent and apply the values to all grid items.

* The `justify-items` property aligns content along the row axis. 
* The `align-items` property aligns content along the column axis. 

The values that the `align-items` and `justify-items` properties take are as follow:
***normal*** For grid items, this behaviour similar to the one of stretch, except for boxes with an aspect ratio or an intrinsic size where it behaves like start
* **stretch**  fills the whole grid area, this is the **default** value, unless item has intrinsic aspect ratio
* **start** aligns the content to the left end or top of the grid area,  this is the **default** value for elements that have an intrinsic aspect ratio
* **end** aligns the content to the right end or bottom of the grid area
* **baseline/first baseline/last baseline** All items are aligned/justified such that their baselines align.([more on this here](https://drafts.csswg.org/css-align/#baseline-values))
* **safe center** if the size of the item overflows the alignment container, the item is instead aligned as if the alignment mode were start
* **unsafe center** regardless of the relative sizes of the item and alignment container, the given alignment value is honoured


If you want a single grid item to have a different alignment, you can use the **`justify-self`** and **`align-self`** properties, which take the same values.

<!-- <img src="https://hychalknotes.s3.amazonaws.com/justify-self.png" width="">
<img src="https://hychalknotes.s3.amazonaws.com/align-self.png" width=""> -->

*Note* _The default behaviour in align-self/align-items is to stretch, except for items which have an intrinsic aspect ratio. If the item does have an intrinsic aspect ratio (like images!) the item will default to start, so as to not stretch and distort the item. This is new to the spec, so browsers haven't rolled this out yet. To protect images and other elements that have intrinsic aspect ratios we can set `align-self` and `justify-self` to `start`._


### Organizing space _around_ the grid
Rarely, you might have a case where your grid doesn't fill the entire grid container. This can happen when you use pixel values for your grid area widths.

In this case, you can use the `justify-content` and `align-content` properties to align the grid within its container. Again, `justify-content`and `align-content` are properties that are defined on the grid parent.

* `justify-content` refers to space on the **row** axis
* `align-content` refers to space on the **column** axis

Here are the values `justify-content`and `align-content` can take:
* `start` aligns the grid to the beginning (left or top). This is the **default** value.
* `end` aligns the grid to the end (right or bottom)
* `center` aligns the grid in the center of the parent
* `stretch` stretches the grid items to fill the parent grid width
* `space-around` places an even amount of space between the grid items, with half spaces around the outside edges
* `space-between` places an even amount of space between the grid items, with no space around the outside edges
* `space-evenly` places an even amount of space between the grid items, with equal space around the outside edges

## Flexbox and Grid
CSS grid does not replace flexbox. It also doesn't replace the flow spec (display block and inline), or even floats! There are times and places for all of the tools we have been using. With the introduction of grid, we have one more tool to add to our kits.

Flexbox and grid were created to solve different problems. Flexbox focuses on content flow whereas grids focus on content placement. Flexbox excels at lining elements up in a single direction while grid always wants to line up items in two directions. Grids allow you to having overlapping content, which is not something that flexbox can do. Flexbox doesn't force content to sit within rigid lines, it is more fluid, but it also doesn't give developers a lot of control over the width of items which grids does. 

![](https://hychalknotes.s3.amazonaws.com/Untitled%20drawing.png)

There are many different philosophies around when to use grid and when to use flexbox. Below, we've outlined just a few, use these as a starting off point fo form your own opinion!

 - It depends on the design: Some developers feel that certain designs are easier to layout in a grid format and some are not. Examine the design you were given carefully and use your knowledge of both methodologies to determine which will work best remembering that flexbox is best for one dimensional 'content flow' situations while grid shines in two dimensional 'content flow' situations.

- Some developers stick to using grid for laying out the larger elements on their page and then use flexbox for smaller sections of their sites where perhaps laying out an entire grid system would be time consuming. However, several prominent members of the CSS community have warned that this approach can lead to using the wrong tool for the job.

- Browser Support: This becomes less of an issue as browsers support more and more layout options but should still be considered when choosing between grid and flexbox.

For more opinions on Grid vs. Flexbox see [this article from CSS Tricks](https://css-tricks.com/quick-whats-the-difference-between-flexbox-and-grid/). 

### Custom grid line names

If we want to, we can also name these lines. We can do this inside of our `grid-template-columns` and `grid-template-rows` properties. The syntax for this is square brackets and our custom name. Names follow class naming conventions, so they can't start with a number and are case sensitive. If we leave out any line names, CSS will name them for us, like we've seen above. Remember we will have an more lines than we do grid areas. We can also give one line two names, just separate them with a space like classes! 

```css
grid-template-columns: [start] 1fr [gutter-end wrapper-start] 800px [wrapper-end] 1fr [end];
grid-template-rows: [top] 100px [middle] 100px [end];
```

### Grid template areas

As if all this wasn't enough, there is another way to create a grid in CSS!

#### `grid-template-areas` and `grid-area`
The `grid-template-areas` property gets set on the parent container of the grid. It specifies the areas of the grid by naming them. Repeating the name of the grid twice, will create an area that spans two columns. We can use a period `.` to create an empty grid area. When defining the grid template area, each row is separated with quotes. If we use a little whitespace, the syntax itself looks like the grid we want to create. Take the following example: 

```css
grid-template-areas: 
  "header header header" 
  "main main aside" 
  "footer footer footer";
```
> There are no commas to separate the rows or areas, just spaces.

In order for this to work, we need to tell the child elements which grid areas to span. We can use the `grid-area` property on the children with the names we gave our areas in the `grid-template-areas` property. 

```css 
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 100px 100px 100px;
  grid-template-areas: 
    "header header aside" 
    "main main aside" 
    "footer footer footer";
  grid-gap: 15px;
}
.gridItem1 {
  grid-area: header;
  background: #80CBC4;
}	
.gridItem2 {
  grid-area: main;
  background: #E8D7FF;
}	
.gridItem3 {
  grid-area: aside;
  background: #63ADF2;
}	
.gridItem4 {
  grid-area: footer;
  background: #FFA630;
}
```

<!-- #### Combining `minmax` with `auto-fit` and `auto-fill`

Combining the `minmax` function with `auto-fit` and `auto-fill` can help create some intuitively responsive layouts. To dig in a bit deeper, you can read this [CSS Tricks Article](https://css-tricks.com/auto-sizing-columns-css-grid-auto-fill-vs-auto-fit).

Another great resource for combining those properties is [this article by Rachel Andrew](https://rachelandrew.co.uk/archives/2016/04/12/flexible-sized-grids-with-auto-fill-and-minmax/), who is a member of the CSS Working Group. -->

## Quirks and gotchas

* Pseudo elements in grid areas? Not yet! 
* You can't add borders or backgrounds to grid areas, just grid elements.
* Nested grids have no way of communicating with parent grids. Ideally, you would be able to line internal grid elements to the parent grid, or other nested grids but not yet!
* `grid-line` number -1 is the end of the explicit grid, not the whole grid!
* Q: Can I make a masonry layout using grid? 
  * A: Not without JavaScript or positioning.
