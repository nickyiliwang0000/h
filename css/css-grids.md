# CSS Grid

CSS Grid is a relatively new layout system available to us. It is a two-dimensional grid-based system, meaning it can handle both columns and rows.


## Creating our grid

To begin, we'll need to set the display property of our parent element. There are two values we can use for this property to help initialize a grid layout system:

* `display: grid;` will give us a grid that is a block level grid

* `display: inline-grid;` will give us a grid that is an inline-block grid

Setting our display property alone won't create a grid for us. Next, we need to tell our grid how to lay out our columns(vertical) and rows(horizontal). To do this, we need to set up our `grid-template-columns` and `grid-template-rows` properties.

### `grid-template-columns` & `grid-template-rows`

These properties take a unit of measurement, sometimes referred to as a _track size_, for each row or column you want to have. We will separate each row or column size with a space only, no commas. 

To begin, let's download [gridStarter.zip](https://hychalknotes.s3.amazonaws.com/gridStarter.zip).

Add the following CSS to our stylesheet:

```css
.container {
  display: grid;
  grid-template-columns: 25% 50% 25%;
  grid-template-rows: 100px 200px;
}
```
Not only can use both pixel values and percentages, but we also have another unit of measurement available. 

### Introducing the `fr` unit

CSS Grid introduces a new unit of measurement called the `fr` unit, meaning **fraction of the free space in the grid container**. The `fr` value is determined after any non-flexible columns or rows are declared. Meaning if you have a five column layout and two columns are already set with `100px` each, and the remaining columns are `1fr` each, the free space will be split up into three fractions and distributed evenly. This is very similar to how the flex grow and flex shrink properties work.

Let's change our CSS to match the following:

```css
.container {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr;
  grid-template-rows: 100px 100px;
} 
```

What happens if we change the second column value to be `300px`? The fr units scale according to the free space available once the rest of the columns have been defined.

## Creating space between grid items

In order to create gaps(sometimes referred to as gutters) between columns and rows, there are two properties available: `grid-row-gap` and `grid-column-gap` which can be condensed into the shorthand `grid-gap`. When using the shorthand, the first value indicates grid-row-gap and the second value indicates grid-column-gap. If you provide one value only, it will apply to both. This property is set on the grid container, and will only give you extra space between grid areas, not on the outter edges.

```css
.container {
  grid-gap: <grid-row-gap> <grid-column-gap>;
}
```

These properties will accept fixed or flexible units which will accomodate whatever dimensions you set your columns and rows to, **unless they are set using percentages**. When we use percentages, those units cannot be overwritten and can result in horizontal overflow. This is why the `fr` unit is so powerful in CSS Grid. 

Let's look at what happens when we add `grid-gap: 40px;` to our grid, and toggling `grid-template-columns` to percentages to see the effect.

```css
.container {
  display: grid;
  grid-template-columns: 25% 50% 25%;
  grid-template-rows: 100px 100px;
  grid-gap: 40px;
} 
```


### Explicit and implicit rows and columns

What happens if we have more items in our grid than we've told our grid about? Let's change our CSS to match:

```css
.container {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr;
  grid-template-rows: 150px 150px;
  grid-gap: 20px;
}
```

Next, copy this Emmet snippet to add more markup, and see how our current grid setup handles the addition content: `.gridItem.gridItem$@7*6>p{Grid Item $@7}`.

Here we have 12 grid items, with three items per column, and only 2 rows. What will happen to the three extra elements?

CSS Grids will automatically fit your new content in a new row. The size of the row will be determined by the content that falls to that new row. These new rows are called _implicit rows_. The rows we do create, are called _explicit rows_.

### `grid-auto-flow`

Notice how the extra grid items get put in a new *row*, not a new *column*? This is because the default value for the `grid-auto-flow` is row. We can adjust this by changing this property to column. We will look at another value dense, a little later, but it will fit items in whereever they can fit!

* **row**: default value
* **column**: any implicit items will create new columns
* **dense**: attempts to fill in holes earlier in the grid


For accessibility, using `grid-auto-flow: dense;` will change the order of your grid items. If the order of your content matters to the users understanding then don't this value.


### `grid-auto-rows`

If you do not explicitly create a column or row, the browser will fit the rest of our elements onto a new line (by default), called an implicit row. To control your implicit rows, you can use the `grid-auto-rows` property. It is possible to provide multiple values for multiple implicit rows. However, Firefox does not currently support multiple values, so it is not recommended.


```css
.container {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr;
  grid-template-rows: 150px 150px;
  grid-gap: 20px;
  grid-auto-rows: 100px;
}
```

With the above code, any implicit rows will be 100px tall.

### `grid-auto-columns`

This property controls the size of implicit columns when `grid-auto-flow` is set to `column`. It can be used the same way as grid-auto-rows property. Firefox also does not support multiple values for this property as well, however other browsers do.

## Dev Tools

Firefox has fantastic CSS Grid inspector tools! Let's dive into them.

When you inspect element on a grid container, you should be able to see a small grid icon next to the `display: grid` rule. If you click on that icon, you will enable the _grid tools_. 

![Inspector tools showing a grid icon next to the css rule display:grid](https://hychalknotes.s3.amazonaws.com/Screen%20Shot%202018-01-13%20at%204.19.56%20PM.png)


Click on the layout tab in your inspector tools, and you will see Grid Display Settings and a small map of your grid. You can hover over the map and see more information about the specific grid area you're hovering.

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

Notice those numbers? Those are grid line numbers. For every column and row we create, we also create grid lines. They start on the top left outside edge of our grid and go to the bottom right outer edge. Explicit and implicit rows and columns get numbered. 


## Grid item placement

### `grid-column-start` and `grid-column-end` / `grid-row-start` and `grid-row-end`

To place our child elements in specific grid locations, we can take advantage of grid line numbers and use the properties `grid-column-start`, `grid-column-end`, `grid-row-start`, and `grid-row-end`. We apply these properties to the grid item, or child to the grid container. The start properties refer to the grid line where you want your grid child's location to start, and the end properties refer to the grid line where you want the grid child to end. These grid placement properties can take a number of different values.

Values these properties can take:

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

* **custom grid line name** if you've named your grid lines in `grid-template-columns` and `grid-template-rows` then you can use the names here
* **span < grid line name >** if you want your grid child to span until it hits the included named grid line(see "Additional learning topics" below).


**Important to note:** 
By default grid will shift content to avoid items overlapping. If an overlapping grid item is in your design, then every item in the grid will need to have an explicit `grid-column-start` and `grid-row-start` value.

### Shorthand Placement

* **grid-column** is the shorthand property for grid-column-start and grid-column-end
* **grid-row** is the shorthand property for grid-row-start and grid-row-end

For both properties above, the first value will specify the starting placement, which can be any of the values types listed above. Then, separate the first and second values with a `/`. The second value will specify the end value.

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


## Repeat keyword

The `repeat` keyword is used inside of the value for `grid-template-columns` and `grid-template-rows` when we want to repeat the value for a number of rows or columns. The `repeat` keyword requires at least 2 values. It looks like this: 

The **first value** that repeat takes is either:
- a positive number, representing the number of columns or rows to create

OR

- a keyword 
	- **`auto-fill`** 
	- **`auto-fit`** 
(detailed explanation of both keywords coming up below)

The **second value** that repeat takes is the size of the columns or rows to be created. Most often you will see this size represented in pixels (eg 200px) or fr units (1fr).

Here are some examples of repeat and what the long hand version of writing this out would look like!

```css
<!-- Three columns of 50px each -->
grid-template-columns: repeat(3, 50px); 
<!-- same as saying: -->
grid-template-columns: 50px 50px 50px;

<!-- Two rows of 1fr each -->
grid-template-rows: repeat(2, 1fr);
<!-- same as saying: -->
grid-template-rows: 1fr 1fr;
```

We can also give repeat more than one value to repeat. Note that the values are only separated by a space. Let's look at an example:

```css
grid-template-columns: repeat(4, 1fr 2fr);
<!-- same as saying: -->
grid-template-columns: 1fr 2fr 1fr 2fr 1fr 2fr 1fr 2fr;
```

### `auto-fit` and `auto-fill`

Repeat is super powerful when used with auto-fit and auto-fill. The difference between the two keywords is very subtle, but has to do with extra whitespace. Both fit as many rows/columns at a certain size as possible, while respecting grid-gaps and at smaller breakpoints, the two act the same. It is only when we have extra whitespace available, that we can notice the difference.

**auto-fill** - Fills the row with as many columns as it can fit at the specified size. New tracks can be empty, they will still take up the space allotted. 

**auto-fit** - The browser will create as many tracks as it can at the specified size, but will collapse them if there are no extra elements to place.


Let's look at an example:


#### `auto-fill`
```css
.grid-container--fill {
  grid-template-columns: repeat(auto-fill, 100px);
}

```
![A screenshot illustrating the auto-fill keyword and how it maintains empty extra columns](https://hychalknotes.s3.amazonaws.com/Screen%20Shot%202018-05-27%20at%202.28.52%20PM.png)

Here, auto-fill is creating 11 tracks at the 100px size. Even though there is no content to fit inside the last three tracks. This can be handy when you need an element to be positioned in the last grid area in the explicit grid. If we were to add `grid-column-end: -1;` to the 7th item, it would live at the end of the row! 

#### `auto-fit`

```css
.grid-container--fit {
  grid-template-columns: repeat(auto-fit, 100px);
}
```




![A screenshot illustrating the auto-fit keyword and how it does not create extra columns](https://hychalknotes.s3.amazonaws.com/Screen%20Shot%202018-05-27%20at%202.29.04%20PM.png)

In the auto-fit example, our explicit grid ends after the 7th spot. We do see that the grid is creating 11 columns, but the 8th - 11th spots are collapsed. If we told our 7th item to end at -1 row, it would be in the exact same spot it is in now! 

## `minmax`

`minmax` is a method that takes two values, a minimum size, and a maximum size. It is used in the `grid-template-columns` and `grid-template-rows` properties, most often as the second value in the repeat function. If we use the fr value as the maximum value in the minmax function, we unlock the power of grids to be responsive by default, without media queries! When we use 1fr as the maximum value, we're telling the track to be at it's largest the whole size of the grid.

Let's look at a simple example before diving in and using minmax inside of the repeat function:

<iframe height='265' scrolling='no' title='simple minmax' src='//codepen.io/tiffanydanielle/embed/NMQmEw/?height=265&theme-id=0&default-tab=css,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/tiffanydanielle/pen/NMQmEw/'>simple minmax</a> by Tiffany Nogueira (<a href='https://codepen.io/tiffanydanielle'>@tiffanydanielle</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

# minmax and auto-fit
Let's look at using minmax and auto-fill and minmax and auto-fit together.

<iframe height='265' scrolling='no' title='auto-fill vs auto-fit' src='//codepen.io/tiffanydanielle/embed/MrLwYp/?height=265&theme-id=0&default-tab=html,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/tiffanydanielle/pen/MrLwYp/'>auto-fill vs auto-fit</a> by Tiffany Nogueira (<a href='https://codepen.io/tiffanydanielle'>@tiffanydanielle</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

When we use minmax with auto-fit and auto-fill we can see some more differences between fit and fill! In the above example, notice what happens to the extra space inside of the grid when we use minmax and auto-fit? The tracks will grow to take up the whole width of the grid! 


Let's do that again!

```html
<section class="grid">
	<p>box1</p>
	<p>box2</p>
	<p>box3</p>
	<p>box4</p>
	<p>box5</p>
	<p>box6</p>
	<p>box7</p>
	<p>box8</p>
	<p>box9</p>
	<p>box10</p>
</section>
```

```css
.grid {
	display: grid;
	grid-gap: 10px;
	grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
}
p {
	width: 100%;
	height: 100px;
	background: darkcyan;
}
```
<video controls="controls">
	<source src="https://hychalknotes.s3.amazonaws.com/Screen%20Recording%202017-09-21%20at%2003.39%20PM.mov">
</video>

<a href="https://css-tricks.com/auto-sizing-columns-css-grid-auto-fill-vs-auto-fit/">Learn more here!</a>




<a href="https://rachelandrew.co.uk/archives/2016/04/12/flexible-sized-grids-with-auto-fill-and-minmax/" target="_blank">This is a great resource on understanding **repeat/auto-fill/auto-fit/minmax**, and how to use them to create a responsive layout.</a>

## Order 
Order in grid is the same as order in flexbox. All grid items have a default of 0, negative order values will make the grid item appear before the rest, a positive number will make the item appear after the rest. 

<div class="accessibility">
Using order on grid items will change the order of your grid items. If the order of your content matters to the users understanding then DO NOT USE this. Hot tip: order in image galleries and articles should be fine. Order on paragraphs would be confusing.
</div>

<iframe height='265' scrolling='no' title='CSS Grid Order' src='//codepen.io/tiffanydanielle/embed/JMwqEa/?height=265&theme-id=0&default-tab=html,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/tiffanydanielle/pen/JMwqEa/'>CSS Grid Order</a> by Tiffany Nogueira (<a href='https://codepen.io/tiffanydanielle'>@tiffanydanielle</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>


## Grid Template Areas
As if all this wasn't enough, there is another way to create a grid in CSS!

### grid-template-areas and grid-areas
The `grid-template-areas` property gets set on the parent container of the grid. It specifies the areas of the grid by naming them. Repeating the name of the grid twice, will create an area that spans two columns. We can use a period `.` to create an empty grid area. When defining the grid-template area, each row is separated with quotes. If we use a little whitespace, the syntax itself looks like the grid we want to create. Take the following example: 

```css
grid-template-areas: 
	"header header header" 
	"main main aside" 
	"footer footer footer";
```
Note: there are no commas to separate the rows or areas, just spaces.

In order for this to work, we need to tell the children elements which grid areas to span. We can use the `grid-area` property on the children with the names we gave our areas in the grid-template-areas property. 

```html
    <div class="container">
        <div class="item">header</div>
        <div class="item">main</div>
        <div class="item">aside</div>
        <div class="item">footer</div>
    </div>
```

```css 
    .container {
        margin: 100px 50px;
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        grid-template-rows: 100px 100px 100px;
        grid-template-areas: 
            "header header aside" 
            "main main aside" 
            "footer footer footer";
        grid-gap: 15px;
    }
    .item:first-child {
        grid-area: header;
        background: #80CBC4;
    }	
    .item:nth-child(2){
        grid-area: main;
        background: #E8D7FF;
    }	
    .item:nth-child(3) {
        grid-area: aside;
        background: #63ADF2;
    }	
    .item:last-child {
        grid-area: footer;
        background: #FFA630;
    }
```
which gives us a layout that looks like this:
![](https://hychalknotes.s3.amazonaws.com/Screen%20Shot%202018-05-27%20at%203.42.56%20PM.png)


**Note** _your grid areas must make sense in order to work. You cannot have an element span two different areas of the grid. Areas must be rectangular for this to work!_ No tetrus allowed!


## Exercise!
Let's get some practice creating a responsive gallery.

Download the starter files here <a href="https://hychalknotes.s3.amazonaws.com/gallery-exercise-start.zip" download>gallery-exercise-start.html</a>.

<a href="https://hychalknotes.s3.amazonaws.com/gallery-exercise-finished.zip" download>If you need it the answer key is here!</a>

<a href="http://tiffanydanielle.ca/grids-gallery">You can also view the completed exercise here.</a>


Once we're finished, let's revisit `grid-auto-flow: dense;` for a minute! 

Go ahead and add a wide class in our css and to the first image with the tall class.

```css
.wide {
	grid-column: span 2;
}
```
```html
<img src="images/greece.jpg" class="tall wide" alt="white painted houses of greece">
```

![](https://hychalknotes.s3.amazonaws.com/Screen+Shot+2018-05-27+at+3.35.04+PM.png)

Notice the empty spot in the right hand corner? Let's add `grid-auto-flow: dense;` to our parent container (the grid element!).

```css
.grid {
	display: grid;
	grid-template-columns: repeat(auto-fill, minmax(400px, 1fr));
	grid-auto-rows: 255px;
	grid-auto-flow: dense;
}
```
Magic! The grid automatically finds an element that will fit in this space, and places it there! This is not so great for items where order matters, but for an image gallery or maybe even independent articles, this could be perfect! 



## Content Sizing Keywords: 
Instead of using a measurement unit or fr in our grid-template-columns or grid-template-rows we can also use content sizing keywords. Let's look at an example of these three keywords outside of grid before diving into a grid example. 

### min-content
min-content will make an element be the smallest width possible. This is usually dictated by the longest word.

<iframe height='265' scrolling='no' title='Content Sizing Keywords : min-content' src='//codepen.io/suzettemccanny/embed/jpwjoP/?height=265&theme-id=0&default-tab=html,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/suzettemccanny/pen/jpwjoP/'>Content Sizing Keywords : min-content</a> by Suzette McCanny (<a href='https://codepen.io/suzettemccanny'>@suzettemccanny</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

### max-content
max-content will let an element be as wide as necessary to fit all of the content. In the case an element can be larger than it's parent, max-content will cause an overflow.

<iframe height='265' scrolling='no' title='Content Sizing Keywords : max-content' src='//codepen.io/suzettemccanny/embed/JBJgdL/?height=265&theme-id=0&default-tab=html,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/suzettemccanny/pen/JBJgdL/'>Content Sizing Keywords : max-content</a> by Suzette McCanny (<a href='https://codepen.io/suzettemccanny'>@suzettemccanny</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

### fit-content
fit-content takes a value that will become the size of the element. Example: `grid-template-columns: fit-content(200px) 1fr 1fr;`

What's great about these keywords, is they are supported in all broswers that also support grids! Let's look at how we can use these in grids:

<iframe height='265' scrolling='no' title='Content Sizing Keywords - fit-content' src='//codepen.io/suzettemccanny/embed/GBMKvZ/?height=265&theme-id=0&default-tab=html,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/suzettemccanny/pen/GBMKvZ/'>Content Sizing Keywords - fit-content</a> by Suzette McCanny (<a href='https://codepen.io/suzettemccanny'>@suzettemccanny</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

## Grid Alignment Keywords
Unlike flexbox, the keywords to organize space on a grid do not change. Justify will always refer to the row axis, and align will always refer to the column axis.

**justify** refers to space on the **row axis**


![](https://hychalknotes.s3.amazonaws.com/justify-row-axis.png)


**align** refers to space on the **column axis.**


![](https://hychalknotes.s3.amazonaws.com/align-column-axis.png)

 
## Controlling space in a grid
### Organizing space _within_ the grid 

#### justify-items and align-items
The `justify-items` and `align-items` properties are set on the grid parent and apply the values to all grid items (cells).

* The `justify-items` property aligns content along the row axis. 
* The `align-items` property aligns content along the column axis. 

The values that the `align-items` and `justify-items` properties take are as follow:
***normal*** For grid items, this behaviour similar to the one of stretch, except for boxes with an aspect ratio or an intrinsic size where it behaves like start
* **stretch**  fills the whole grid area, this is the **default** value, unless item has intrinsic aspect ratio
* **start** aligns the content to the left end or top of the grid area,  this is the **default** value for elements that have an intrinsic aspect ratio
* **end** aligns the content to the right end or bottom of the grid area
* **baseline/first baseline/last baseline** All items are aligned/justified such that their baselines align. (<a href="https://drafts.csswg.org/css-align/#baseline-values" target="_blank">more on this here</a>)
* **safe center** if the size of the item overflows the alignment container, the item is instead aligned as if the alignment mode were start
* **unsafe center** regardless of the relative sizes of the item and alignment container, the given alignment value is honoured

<!-- <img src="https://hychalknotes.s3.amazonaws.com/justify-items.png" width="500px">


<img src="https://hychalknotes.s3.amazonaws.com/align-items.png" width="500px"> -->

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
* **start** aligns the grid to the beginning (left or top). This is the **default** value.
* **end**  aligns the grid to the end (right or bottom)
* **center** aligns the grid in the center of the parent
* **stretch** stretches the grid items to fill the parent grid width
* **space-around** places an even amount of space between the grid items, with half spaces around the outside edges
* **space-between** places an even amount of space between the grid items, with no space around the outside edges
* **space-evenly** places an even amount of space between the grid items, with equal space around the outside edges

<!-- <img src="https://hychalknotes.s3.amazonaws.com/justify-content.png" width="">
<img src="https://hychalknotes.s3.amazonaws.com/align-content.png" width=""> -->

<a href="https://hychalknotes.s3.amazonaws.com/grid-cheatsheet.pdf" download>Download your cheatsheet here</a>

## Exercise
Let's try to build a flexible and responsive website layout with CSS grid!

Download the starter files here <a href="https://hychalknotes.s3.amazonaws.com/hero-3x-exercise-START.zip"> hero-3x-exercise-START.html</a>

<a href="https://hychalknotes.s3.amazonaws.com/hero-3x-exercise-FINISHED.zip ">Here is the answer key!</a>


## Browser Support
<a href="https://css-tricks.com/another-collection-of-interesting-facts-about-css-grid/" target="_blank">https://css-tricks.com/another-collection-of-interesting-facts-about-css-grid/</a>

Browser support for CSS grids is pretty good. <a href="http://caniuse.com/#search=grid" target="_blank">Check out the latest support here. </a>

**We currently (as of May 2018) have support for 87% of all global users.** Of course, this can change for individual sites. 

All evergreen browsers do support grid!

You'll notice that IE 10 and 11 have partial support for grid. What does this mean? These browsers supported the earliest spec of grid with a prefix (-ms-) and sometimes different property names. Here are a few examples of flagged grid properties:

* grid-template-columns as -ms-grid-columns
* grid-template-rows as -ms-grid-rows
* grid-row-start as -ms-grid-row
* grid-column-start as -ms-grid-column
* align-self as -ms-grid-row-align
* justify-self as -ms-grid-column-align

The newer features in grid are not supported in these browsers. Things like auto placement, grid-template-areas layouts, and grid-gap are new, and not supported in these browsers. There are solutions to this, but we will have to use some other tools to get the job done! 

<a href="https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/CSS_Grid_and_Progressive_Enhancement#The_Internet_Explorer_and_Edge_situation" target="_blank">Read more about the IE situation here!</a>

## Solutions 

### Autoprefixer 
For those who are new to tools in web dev, autoprefixer is a tool that automates the addition of flags (prefixes) for us. It knows which properties need browser flags in order to work. This can help with some grid support, although we're going to need more than just autoprefixer if we want to use the newest grid spec and the new features of grid! 

Autoprefixer **doesn't** automatically prefix grid properties. If we want it to, we need to tell autoprefixer to turn on autoprefixing for grid! <a href="https://github.com/postcss/autoprefixer#user-content-features-1" target="_blank"> Read the autoprefixer docs here!</a>

<a href="https://rachelandrew.co.uk/archives/2016/11/26/should-i-try-to-use-the-ie-implementation-of-css-grid-layout/" target="_blank">This is a great article by Rachel Andrew explaining exactly what is supported in IE and how to use autoprefixer.</a>

<a href="https://docs.microsoft.com/en-us/previous-versions/windows/internet-explorer/ie-developer/dev-guides/hh673533(v=vs.85)" target="_blank">Here is a microsoft article outlining how to use grid layout on their older browsers.</a>

### Progressive Enhancement
Progressive Enhancement is a strategy for web development that says we first ensure **all users** can experience web content, and only enhance that experience when we know we are able to. It requires devs to build a solid product using only the most basic tech that all users can use, and only afterwards enhance the experience with new tech for users who will be able to benefit. 

To use progressive enhancement with grid, we would first ensure our layout works for all users and all browsers - maybe by building it with floats or flexbox - and then the browsers that can support grid will get a more complex layout. How do we do this? Enter **feature queries!**

<a href="https://www.smashingmagazine.com/2009/04/progressive-enhancement-what-it-is-and-how-to-use-it/" target="_blank">Read more about progressive enhancement here!</a>



### Feature Queries

Feature Queries are a specific query that checks support of CSS properties. These are similar to media queries, which will check for the viewport size and run only that code if the browser matches this size. 

With feature queries, we ask the browser to check to see if a certain feature is supported, and if it is, only then run the following code. If the feature is not supported, then the code will be ignored. If we use clever CSS fallbacks by taking advantage of **cascading,** we can ensure all browsers display a nice layout for all of our users.

Consider the following:

```css
div .child {
	float: left;
	width: 33%;
}

@supports (display: grid) {
	div .child {
		float: none;
		width: auto;
	}
	div {
		display: grid;
        	grid-template-columns: 1fr 1fr 1fr;
	}
}
```


### Example of Progressive Enhancement in the wild!

* <a href="https://s.codepen.io/matuzo/debug/Emddvx" target="_blank">Check out this example of progressive enhancement and grid by Manuel Matuzović.</a>

* <a href="https://www.smashingmagazine.com/2017/07/enhancing-css-layout-floats-flexbox-grid/" target="_blank">You can read his article on Smashing Magazine about the layout here!</a>

<a href="https://developer.mozilla.org/en-US/docs/Web/CSS/%40supports" target="_blank">Read more here.</a>

<a href="https://hacks.mozilla.org/2016/08/using-feature-queries-in-css/">More about how it _works_ here!</a>

When we add `display: grid;` to a parent, we override any floats and clears. This doesn't change the fact we need to change the width on the children - width will now be overridden.

**Fun Fact:** 
Rachel Andrew recommends using flexbox as the main fallback for grid. As if we live in a world where flexbox is the fallback?!


##Flexbox vs Grid
While Flexbox is only concerned with one axis, CSS grids are concerned with both axes. Have you ever wanted to change the position of one item on the main axis in flexbox? Align-item exists, but this is for the opposite axis. There is no justify-item in flexbox! Enter grids!

CSS grid does not replace flexbox. It also doesn't replace the flow spec (display block and inline), or even floats! There are times and places for all of the tools we have been using. With the introduction of grid, we have one more tool to add to our kits.


## Grid vs Flexbox
<a href="https://rachelandrew.co.uk/archives/2016/03/30/should-i-use-grid-or-flexbox/" target="_blank">Here is a great article outlining when you should use grid vs flexbox</a>

Think about your problem, do you want your content to dictate the way the element is displayed in a row or in a column? If so, use flexbox. Do you want to use a grid and position grid items yourself? If so, use grid! 

See the below examples from <a href="https://www.smashingmagazine.com/2017/09/css-grid-gotchas-stumbling-blocks/" target="_blank">Rachel Andrew's article on grid gotchas:</a>

### When to use grid:
- Grid is great at controlling content in two dimensions - **in rows AND columns.**
- Grid allows us to overlap our items! 

If you can take your layout or component and draw a grid over it, with rows and columns. It is two-dimensional — use grids!
<img src="https://hychalknotes.s3.amazonaws.com/Screen%20Shot%202018-01-14%20at%208.24.42%20PM.png" width="500px">





## Quirks and Gotchas

* Pseudo elements in grid areas? Not yet! 
* can't add borders and backgrounds to grid-areas, just grid elements
* Nested grids have no way of communicating with parent grids. Ideally, you would be able to line internal grid elements to the parent grid, or other nested grids but not yet!
* -1 is the end of the explicit grid, not the whole grid!
* Can I make a masonry layout? Not without Javascript or positioning
* Need to make perfectly square elements? <a href="https://css-tricks.com/things-ive-learned-css-grid-layout/#article-header-id-5" target="_blank"> Read about using the vmin measurement to do so here!</a>


## Additional learning topics

### Custom Grid Line Names

If we want to, we can also name these lines. We can do this inside of our grid-template-columns and grid-template-rows properties. The syntax for this is square brackets and our custom name. Names follow class naming conventions, so they can't start with a number and are case sensitive. If we leave out any line names, css will name them for us, like we've seen above. Remember we will have an more lines than we do grid areas. We can also give one line two names, just seperate them with a space like classes! 

```css
grid-template-columns: [start] 1fr [gutter-end wrapper-start] 800px [wrapper-end] 1fr [end];
grid-template-rows: [top] 100px [middle] 100px [end];
```

### When to use flexbox:
- Flexbox is great at controlling content - **in a row OR in a column.**
- Items flow one after another, never overlapping

If instead, you want individual items to expand within a row, without respecting what happens in the row above. That's a flex layout.
<img src="https://hychalknotes.s3.amazonaws.com/Screen%20Shot%202018-01-14%20at%208.24.50%20PM.png" width="500px">


### Gap in Flexbox?!

A recent addition to the Box Alignment specification has been the row-gap and column-gap properties, along with the shorthand gap. These properties were initially defined in the CSS Grid specification and named grid-row-gap, grid-column-gap and grid-gap. They have been renamed and moved to Box Alignment in order that they can be used in all layout methods — this will ultimately include **flexbox**. Until browsers implement the gap properties for flexbox, margins have to be used to create gaps between items.

<a href="https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Relationship_of_Flexbox_to_Other_Layout_Methods">Read more here!</a>