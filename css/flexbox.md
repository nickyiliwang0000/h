<!-- Student takeaway -->
<!-- By the end of this lesson, the student should know:
- That display:flex is set on the parent of the flexed items
- That flex-direction sets the main axis
- That justify-content orients items along the main axis
- That align-items orients items along the secondary axis
- That align-content arranges content within the context of the flex container AND it only applies if there is more than one line of content
- That align-self and order are for one offs
- How to center something with flexbox
-->

# Flexbox
By now, we're comfortable achieving layout through widths and floats and working with pixels and percentages for sizing. However, using floats for layouts can produce really difficult challenges: things like vertical centering require relatively many lines of (kinda hacky) code.

Enter 🙌 _flexbox_ 🙌. Flexbox solves many float layout issues elegantly.

As of today, [the browser support for flexbox](http://caniuse.com/#search=flex) is great! However, there will be issues with older versions of IE, and we should use vendor prefixes to support older versions of Chrome, Safari, and Firefox. 
<!-- For the examples throughout this lesson, we'll use vendor prefixes for IE. -->

## Using flexbox
To get started, download the starter files [here](https://hychalknotes.s3.amazonaws.com/learning-flexbox.zip). We will be using these files throughout the lesson.

### `display: flex;`
In order to use flexbox in a layout, we must have the elements we want to lay out inside their own container. We will apply a `display: flex;` property to this container element. 

```css
.flexContainer {
  display: flex;
}
```

### `flex-direction`
You know how when we say `position: absolute;` on an element, we unlock the ability to use the `top`, `right`, `bottom` and `left` properties Something similar happens when we set a container to `display: flex;`. We now have access to a bunch of properties that will describe how the content inside the container behaves.

The default behavior of all child elements of a parent that is `display:flex;` is for them to flow next to each other. 

Child elements are positioned along a main axis. We can choose this axis using the `flex-direction` property. When we choose a main axis, the other axis becomes _the secondary axis_.

### `flex-direction:row;`
Setting `flex-direction` to `row` will make the X axis (horizontal) the main axis. Your content will flow **left to right**.

![FlexDirectionRow](http://fulltime.hackeryou.com/assets/flexbox/flexDirectionRow.jpg)

(This is the default.)

### `flex-direction:row-reverse;`
Setting `flex-direction` to `row-reverse` will make the X axis the main axis. Your content will flow **right to left**.

![FlexDirectionRowReverse](http://fulltime.hackeryou.com/assets/flexbox/flexDirectionRowReverse.jpg)

### `flex-direction:column;`
Setting `flex-direction` to `column` will make the Y axis the main axis. Your content will flow **top to bottom**.

![FlexDirectionColumn](http://fulltime.hackeryou.com/assets/flexbox/flexDirectionColumn.jpg)

### `flex-direction:column-reverse;`
Setting `flex-direction` to `column-reverse` will make the Y axis the main axis. Your content will flow **bottom to top**.

![FlexDirectionColumnReverse](http://fulltime.hackeryou.com/assets/flexbox/flexDirectionColumnReverse.jpg)

## Arranging content within a flexed container

`justify-content` is used to position the contents along the **main axis**.

`align-items` defines how content is positioned along the **secondary axis**. (The default is `stretch`, which means that a column will take up the full width of its parent.)

With both properties, `flex-start` and `flex-end` can be used to position accordingly. 

### `justify-content: flex-start`
```css
.flexContainer {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
}
```

![justify-content: flex-start; with numbered boxes. They begin at the upper left corner of the parent container.](https://hychalknotes.s3.amazonaws.com/01-flexbox-jc-fs-min.png)

### `justify-content: flex-end`
```css
.flexContainer {
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
}	
```
![justify-content: flex-end; with numbered boxes. They begin at the upper right corner of the parent container.](https://hychalknotes.s3.amazonaws.com/02-flexbox-jc-fe-min.png)


### `align-items: flex-start`
```css
.flexContainer {
  display: flex;
  flex-direction: row;
  align-items: flex-start;
}	
```
![align-items: flex-start; with numbered boxes. They begin at the upper left corner of the parent container.](https://hychalknotes.s3.amazonaws.com/03-flexbox-ai-fs-min.png)

### `align-items: flex-end`
```css
.flexContainer {
  display: flex;
  flex-direction: row;
  align-items: flex-end;
}
```
![align-items: flex-end; with numbered boxes. They begin at the lower left corner of the parent container.](https://hychalknotes.s3.amazonaws.com/04-flexbox-ai-fe-min.png)

## Spacing content

### `justify-content: space-between;`
Setting `justify-content` to `space-between` will position the content so that the first line is at the start of the container, and the last line is at the end.

```css
.flexContainer {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
```

![justify-content: space-between; with numbered boxes. The outer edges of the first and last boxes touch the container's border.](https://hychalknotes.s3.amazonaws.com/05-flexbox-jc-sb-min.png)


### `justify-content: space-around;`

Setting `justify-content` to `space-around` will position the content so that the empty space before the first and after the last item equals half of the space between each pair of adjacent items, giving them the appearance of equal margins.

```css
.flexContainer {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}
```

![justify-content: space-between; with numbered boxes. Each box has the same amount of space around it on all sides.](https://hychalknotes.s3.amazonaws.com/06-flexbox-jc-sa-min.png)

## Combining spacing properties
`justify-content` and `align-items` can be used together as well to position elements where they are needed.

```css
.flexContainer {
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
  align-items: flex-end;
}	
```

![justify-content: flex-end;, align-items:flex-end; with numbered boxes.The boxes are positioned at the lower right corner of the parent container.](https://hychalknotes.s3.amazonaws.com/07-flexbox--min.png)

One of the many great benefits of flexbox is that you can easily center content vertically and horizontally.

We use `justify-content` to center along the main axis and `align-items` to center along the secondary axis.

### `justify-content: center;`

```css
.flexContainer {
  display: flex;
  flex-direction: row;
  justify-content: center;
}	
```

![justify-content: center; with numbered boxes. The boxes are positioned at the middle top of the parent container.](https://hychalknotes.s3.amazonaws.com/08-flexbox-min.png)

### `align-items: center;`
```css
.flexContainer {
  display: flex;
  flex-direction: row;
  align-items: center;
}	
```

![align-items:center; with numbered boxes. The boxes are positioned at the left middle of the parent container.](https://hychalknotes.s3.amazonaws.com/09-flexbox-min.png)

These together give us:

```css
.flexContainer {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}	
```

![align-items:center; justify-content:center; with numbered boxes. The boxes in the exact middle the parent container.](https://hychalknotes.s3.amazonaws.com/10-flexbox-min.png)

Lovely centering!

We can also give `margin: auto` to the **element** we want to center.

```css
.flexContainer {
  display: flex;
  flex-direction: row;
}

.flexItem {
  margin: auto;
}
```

## Adjusting white space

Add a new rule to `.flexContainer` in your file: `width: 300px;`.

When working with floats, we expect our elements to wrap to the next line when they don't fit in the parent space. This is not the case with flexbox: when we have many elements inside of a parent container, they resize to fit the space.

In order to fix this weirdness, we need to state that the elements will wrap to the next row or column (depending on what we set as the main axis) using `flex-wrap: wrap;`.

```css
.flexContainer {
  display: flex;
  height: 300px;
  width: 300px;
  border: 2px solid #333;
  flex-wrap: wrap;
}
```

Toggle between `flex-direction: column;` and `flex-direction: row;` and see how that changes the way the content flows.

In the previous examples, we've had to deal with a lot of white space around the elements. Flexbox also provides us with some properties to better control how we can utilize this extra spacing. (Note that the following rules only apply when there is **more than one row or column of content** (depending on the `flex-direction`).

### `align-content: space-between;`

Setting `align-content` to `space-between` will position the content so that the first line is at the start of the container, and the last line is at the end.

### `align-content: space-around;`

Setting `align-content` to `space-around` will position the content so that the empty space before the first and after the last item equals half of the space between each pair of adjacent items, giving them the appearance of equal margins.

> You may see `space-evenly`, which can be useful, but currently [is only supported in Firefox](https://www.bram.us/2017/07/18/justify-content-space-evenly-for-flexbox/).

### `align-content: flex-start;`

Setting `align-content` to `flex-start` packs the content to the start of the container along the main axis.

### `align-content: flex-end;`

Setting `align-content` to `flex-start` packs the content to the start of the container along the main axis.


## Special cases

### `align-self`

Setting `align-self` will overwrite the inherited or default position of a child of a flex container along the secondary axis.

(Note that, in opposition to `align-content`, `align-self` only applies when there is **one row or column of content** (depending on the `flex-direction`).

Go to your code and add the following CSS:

```css
.flexItem:last-child {
  align-self: flex-end;
}
```

### `order`

By default, children of flexed parents are laid out in the order they appear in the markup. Setting the `order` property to an integer value (e.g. `10`, `3`, `-1`) on a specific element will appear to move that item. By default, each element has a value of `0`. Elements are laid out in the ascending order. If two flex child elements have the same `order` value, they will appear in on screen in order they appear in the markup.

Add a class of `.lastNameStartsWithA` to a `.flexItem` in the middle of the group:

```css
.lastNameStartsWithA {
  order: -1;
}
```
See how it pops to the front of the line?

The `order` property only affects the **visual order** of elements (not the actual markup). Screen readers will still read the elements in the order they appear in the markup.

Check out [more about order](https://developer.mozilla.org/en/docs/Web/CSS/order).

## Flexbox fluidity
Flexbox was built in response to the move toward responsive web design and development. Knowing that content will change size in response to the side of the browser is why flexbox's developers created the `flex` property.

### `flex: 1 0 auto;`
Setting `flex` to `1 0 auto` is shorthand for `flex-grow: 1;`, `flex-shrink: 0;`, and `flex-basis: auto;`, which describes how the element will resize when the parent container does.

### `flex-grow` 
The value of this property is a unitless value that represents how much the element will grow in relation to the other elements in its container when its container grows.

[Confused](https://css-tricks.com/flex-grow-is-weird/)?

### `flex-shrink`
The value of this property is a unitless value that represents how much the element will shrink in relation to the other elements in its container when its container shrinks.

It is often set to 0 to indicate that the element should **not** shrink. Add `flex-shrink:0;` to our 100px-wide `.flexItem:last-child`. See how it doesn't get smaller than 100px even when the browser window smooshes?

You can download and play around with [this great example](https://hychalknotes.s3.amazonaws.com/flex-shrink-example.html) of a nav that uses `flex-shrink`.

Visit the [documentation on MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-shrink) for a detailed example of `flex-shrink`.

### `flex-basis`
The value of this property is the ideal size of the element. It can be declared in pixels or percentage. As you've seen, once items are placed in a flexbox, their dimensions can change.

Go to your file and add the rule `flex-basis: 100px;` to `.flexItem:last-child`. See how it got up to 100px if there is space for it to do so?

[This article](http://gedd.ski/post/the-difference-between-width-and-flex-basis/) does a great job explaining the difference between `width` and `flex-basis`.


## Flexbox code-alongs
We'll download [a starter file](https://hychalknotes.s3.amazonaws.com/flex.html) to see how the flexbox can be used to create a common website layout we've previously made with floats.

Then, we'll get into [flexboxCodeAlong.zip](https://hychalknotes.s3.amazonaws.com/flexboxCodeAlong.zip). We'll use these files to build an advanced layout. 

## Resources

* [Flexbox CheatSheet Visualized (PDF)](http://jonibologna.com/content/images/flexboxsheet.pdf), an excellent flow chart about how to lay out projects with flexbox and what each property does.
* [Flexbox Reference (Codrops)](http://tympanus.net/codrops/css_reference/flexbox/)
* [Solved by Flexbox](http://philipwalton.github.io/solved-by-flexbox/), a bunch of examples of the problems that flexbox has solved for individual developers.
* [Learn CSS Flexbox](http://learnlayout.com/flexbox.html)
* [CSS Tricks guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
* [What The Flexbox?!](https://flexbox.io/), a series of free videos about flexbox by Wes Bos.
* [Flexbox Froggy](https://flexboxfroggy.com/), a flexbox game.
* [Flexbox Zombies](https://flexboxzombies.com/p/flexbox-zombies), another flexbox game!
