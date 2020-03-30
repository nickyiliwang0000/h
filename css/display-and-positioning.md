<!-- Student takeaway: -->
<!--Student will be able to:
- Name the values of the display property (inline, inline-block, block, none)
- Name the values of the position property (static, relative, absolute, fixed)
- Understand that an absolutely positioned element's closest parent contains it
- Understand that positioning is for tweaks, not entire layouts
- Understand that z-index arranges elements on along the z-axis
 -->

# Display and positioning

## The `display` property
Let's take a look at some markup:

```html
<span>inlines</span>
<span>inlines</span>
<span>inlines</span>
<div>BLOCK</div>
<div>BLOCK</div>
<div>BLOCK</div>
```

How will the above be displayed in the browser? Let's open [displayExample.html](https://hychalknotes.s3.amazonaws.com/displayExample.html) in the browser and check it out. (The elements have a teal background and some margin added to see their shape better.)

Why do the spans line up beside each other and the divs start on a new line when their contents are almost identical?

![Screen shot showing the difference between display and inline block, where inline elements are sitting next to each other, and block level elements are stacked.](https://hychalknotes.s3.amazonaws.com/displayExample-screenshot.png)

Because the default display value for `span` is `inline` and the default display value for `div` is `block`. 

The `display` property specifies the type of box that will be used when rendering an element on the page - a box that takes up only the space it needs, or a box that takes up the whole line.

### `display: inline;`
Elements that have the `display:inline;` property (hereafter called _inline elements_) can be nested inside elements that have the `display:block;` property (hereafter called _block elements_).

Write the following HTML inside of `displayExample.html`:

```html
<p>My favourite foods are <span class="food">pho</span> and <span class="food">deviled eggs</span>. Read <em>more</em> about me on my <a href="http://mywebsite.com">website</a>!</p>
```

Notice how we wrapped different words in an `a` or an `em` or a `span` and everything stays in a line in the browser rather than breaking on to a new line? That's because by default, these elements are `display:inline;`.

1. Set a width of 400px on `span.food`. What happens?
2. Try changing the `span` tags to `div` tags. See what happens.

Inline elements do not accept a width because their default behaviour is to only take up as much space as they need and continue on with the content within that element.

### `display:block;`

Block elements break onto a new line. Block elements are often the containers for inline elements. Block elements accept a width, which is why we use them to lay out our pages.

Some examples of block elements are `div`, `h1-h6`, `p`, `ul/ol`, `li`, and `blockquote`

### `display: inline-block;`

`display:inline-block;` is the best of both worlds: you can set a width or height on the element, like you can on a block element, but it will still display side-by-side in the line, like an inline element does. 

Images are the only element that are by default `display:inline-block;`. 

Let's see how it works with some markup (also available in [this CodePen](https://codepen.io/zkdan/pen/BGpEGP))

```html
<p>Here is a picture of a true National Treasure: <img class="myStar" src="https://www.placecage.com/100/100">. Isn't it nice?</p>
```
If we wanted to set a width and height on the image, no problem! It doesn't break to a new line.

### `display:none;`

`display` can also have the value of `none`. It does exactly what you might think it does: hides the element entirely. The space that the element would take up is removed as well, and any subsequent content takes up the space that is available.

Screen readers won't read elements with their `display` properties set to `none`. It's like deleting an element without deleting it.

#### `display: none;` vs. `visibility: hidden;`

`visibility: hidden` is another property that **appears** to perform the same task as `display: none`. But when using `visibility: hidden`, the space the element would take up remains. It's like a chameleon blending into a branch it's sitting on. It's still there, but you can't see it. `display:none;` is like taking the chameleon off the branch. Any elements that have either `display: none` or `visibility: hidden` will not be read by screen readers.

### Hiding elements

There are a few ways of hiding elements, but they all have impacts on accessibility. If you want to hide an element but have it read by a screen reader we recommend using some custom CSS often referred to as `sr-only` or `visually-hidden`. The best practice for this could evolve over time, but the currently recommended CSS for this class is:

```css
.visually-hidden:not(:focus):not(:active) { 
  position: absolute !important;
  height: 1px; 
  width: 1px;
  overflow: hidden;
  clip: rect(1px 1px 1px 1px); /* IE6, IE7 */
  clip: rect(1px, 1px, 1px, 1px);
  white-space: nowrap; /* added line */
}
```
We recommend adding this to your code snippet if you don't already have it ready. Adding this class to any HTML element will ensure that the element is available for assistive technology while staying visually hidden. 


## Positioning your elements

So far, we've been working with `float` or `display` to make elements fit snugly beside each other. This works great most of the time. But what if we want to:

1. Bump something up and over a few pixels?
1. Overlap two elements?
2. Have something burst out of its wrapper?
1. Place an element in the top right corner of a page, regardless of how wide or tall its containing `div` is? (Like an `x` to exit a modal box)
1. Overlap text on top of an image?

>As you may be able to tell from this list, positioning is a tool to use when making stylistic tweaks, **not** for laying out entire pages.

### Element positions

All elements in HTML are by default `position:static;` which means that they aren't positioned at all, they just **take up the space they need** and other elements start after them.

This is what we have worked with so far. You won't need to set `position:static;` on an element unless you are overriding something you have set earlier.

#### `position: relative;`

`position: relative;` acts just like what we are used to (static) but there is one major difference. The element still takes up the space it needs to, but when an element has the property `position:relative;`, it unlocks the ability to use four more properties: `top`,`right`,`bottom`,`left`. These can be used to nudge the element around.

Open [positionRelative.html](https://hychalknotes.s3.amazonaws.com/positionRelative.html) in your editor and do the following:

1. Set the position of the `div.text` to relative.
1. Give the properties `top` and `left` a value of 100px each.
1. Try a negative left value (-100px).
1. Replace `top` with `margin-top`. What is the difference?
<!-- 1. Now try those with the width value of `div.box` at 120%. -->

Where exactly are `top`, `left`, `right` and `bottom` referring to? 
> They refer to the original position of the element!

#### `position: absolute;`

`position: absolute` is another way of positioning elements on a page. When you position an element absolutely, it no longer takes up the space it used to and is now essentially 'floating' on your screen, above the surrounding elements.

You can position an element with `position:absolute;` exactly where you want it to go. Open [positionAbsolute.html](https://hychalknotes.s3.amazonaws.com/positionAbsolute.html) in your browser and editor. Here we have four `div` tags that are 100px square, and they're all `position:static` (the default).

Go ahead and set `.blueBox` to `position: absolute;`:

```css
.blueBox {
    background: rgba(65, 105, 255, 0.7);
    position: absolute;
}
```

What just happened? Where is the `.redBox`? Where did the picture of meat go?

The box with a blue border was set to `position: absolute;` and no longer takes up any space, so the box with the red border bumps itself right up and under the box with the blue border. Since the background of each `div` is not transparent, you can't see any of the box with the red border behind it. If we were to add opacity for all of our `div` elements, what do we see?

Let's use `top` and `left` to position the blue box:

```css
.blueBox {
    border: 2px solid rgba(65, 105, 255, 0.7);
    position: absolute;
    top: 500px;
    left: 120px;
}
```
Or `bottom` and `right` values:

```css
.blueBox {
    background: 2px solid rgba(65, 105, 255, 0.7);
    position: absolute;
    bottom: 20px;
    right: 20px;
}
```

We can also use percentages:

```css
.blueBox {
    background: rgba(65, 105, 255, 0.7);
    position: absolute;
    width: 5%;
    height: 5%;
    top: 45%;
    left: 45%;
}
```

You'll notice that the box can be positioned at any point on the screen. It doesn't care if there is content where it wants to go or not, it just overlaps everything.

Now, what do you think `top`, `left`, `right` and `bottom` are referring to?
> They're referring to the viewport!

##### Practical examples of absolute positioning

It can be hard to visualize what absolute positioning looks like in a real-world example. The bellow graphics can help illustrate some practical use cases:

![Position absolute image example](https://hychalknotes.s3.amazonaws.com/practical-position-absolute.jpg)

##### Combining `position: relative;` and `position: absolute;`

The last example was good for understanding absolute positioning, but it's unlikely that all your elements are direct children of the body like that. You'll probably have a wrapper, a sidebar, (or some other kind of container) and some content between your elements and the body.

This is where we need to mix relative and absolute positioning. Open up [positioning.html](https://hychalknotes.s3.amazonaws.com/positioning.html) in your browser and editor.

Let's write some code so the blue box is positioned like this:

![blue box peeking out from wrapper](https://hychalknotes.s3.amazonaws.com/positionAbsoluteExample.png)

Our first thought may be to do something like this:

```css
.box2 {
    background: rgba(2, 17, 77, 0.7);
    position: absolute;
    top: -20px;
    right: 20px;
}
```

And that's a great instinct! But why is the box positioned waaaaay outside of the wrapper `div`? Try resizing your browser. 🙄  That's annoying. We want the blue box to be positioned to the top right of the wrapper, not the body!

Here is the power of mixing `relative` and `absolute`:

>When you set the position of an element to absolute and use `top`, `right`, `bottom`, `left`, it is absolutely positioned **with respect to its closest parent that has a position other than static.**

So, because we do not have any parent elements set to `relative`, the blue box's positioning is with respect to the the browser window.

An easy fix for this is to change the `position` of our `.wrapper` to `relative`:

```css
.wrapper {
    width: 400px;
    margin: 50px auto;
    border: 2px solid firebrick;
    /* This relative position will contain 
    the absolutely positioned child elements within this box. 
    They will still be absolutely positioned, 
    but now with respect to this box, 
    rather than the body. */
    position: relative; 
}
```

##### Another example

Let's take another shot at this. Open up [positioning2.html](https://hychalknotes.s3.amazonaws.com/positioning2.html) in your browser and editor.

Here we have two divs nested inside of each other: `.wrapper` and `.innerWrapper`

We want to end up with something that looks like this:

![four squares sitting inside the corners of two rectangle outlines](https://hychalknotes.s3.amazonaws.com/positioning2-Example.png)

Our first step would be to position all the boxes absolutely and put them in the 4 corners:

```css
.box {
    width: 100px;
    height: 100px;
    margin: 5px;
    position: absolute;
}
.box1 {
    background: rgba(116, 27, 42, 0.7); /*semi transparent magenta*/
    top: 0;
    left: 0;
}

.box2 {
    background: rgba(2, 17, 77, 0.7); /*semi transparent blue*/
    top: 0;
    right: 0;
}

.box3 {
    background: rgba(166, 157, 2, 0.7); /*semi transparent yellow*/
    bottom: 0;
    left: 0;
}

.box4 {
    background: rgba(0, 69, 0, 0.7); /*semi transparent green*/
    bottom: 0;
    right: 0;
}
```
So why are the boxes in the corners of the browser even though they are nested inside of two wrapper divs?

![four squares sitting outside the corners of two rectangle outlines](https://hychalknotes.s3.amazonaws.com/positioning2-Example2.png)

That is because both wrapper divs are at their default position of `static` and not `relative`.

#### `position: fixed;`

`position:fixed;` is similar to `position:absolute` except that it stays in place when you scroll.

Let's open up [positionFixed.html](https://hychalknotes.s3.amazonaws.com/positionFixed.html) in your browser and editor.

We have a black header at the top. Let's try and use CSS to make it fixed when we scroll:

```css
.fixedHeader {
    width: 100%;
    position: fixed;
    left: 0;
    top: 0;
}
```

Now scroll down. See how the header sticks in place?

When an element is fixed, we need to provide a width because by default it will only take up the width of the content. The space it used to take up disappears, like when you an element has `display:none;` or is positioned with `float`. 

### Z-index

In one of the earlier exercises, we saw elements overlap each other. What if we want them to overlap another way? How do we specify which element goes on top and which one goes under?

We are used to working with X and Y coordinates in web design but now we need to think of elements on the third axis; the Z axis. The Z axis is depth. 

![XYZ axes image from https://vanseodesign.com/css/css-stack-z-index/](https://hychalknotes.s3.amazonaws.com/z-index.png) 

Think of the Z index as a drawer in a filing cabinet. At the very back is file 1 and every file in front of it has a larger value. The first file you can touch when you open the drawer will be the biggest number; it could be, like, 9999 if there are lots of files in the drawer. If there are only two files, the first file you touch will only be number 2, but it's still in front.

`z-index` is a property that describes where an element is in the browser on the Z axis. 

>The z-index property will only take effect if the element also has a `position` value of `absolute`, `relative` or `fixed`.

Open up [z-indexExercise.html](https://hychalknotes.s3.amazonaws.com/z-indexExercise.html) and you'll see we have our four blocks back.

They are all positioned absolutely and are overlapping each other. By default, the order in which they appear in the HTML determines the order in which they overlap. The first element in the HTML has the lowest z-index (i.e. it is farthest back in the filing cabinet) and the last element has the highest (i.e. it is closest to the front of the filing cabinet). We can manipulate that order by changing the value of the `z-index` property.

![overlapping squares with green, red, blue, and orange borders](https://hychalknotes.s3.amazonaws.com/z-indexExample.png)

Let's use `z-index` to bring the red box on top of everything else:

```css
.box3 {
    /*meat picture*/
    border: 2px solid rgb(255, 0, 0);
    top: 60px;
    left: 60px;
    z-index: 1;
}
```
See how the red box is now above everything else? 

Try changing the orange box to `z-index:2;`.

![overlapping squares with green, red, blue, and orange borders](https://hychalknotes.s3.amazonaws.com/z-indexExample2.png)

## Code-along
Let's see how `postion: relative` and `position: absolute` could be used to elevate a design! Download [relative-absolute-code-along--bootcamp.zip](https://hychalknotes.s3.amazonaws.com/relative-absolute-code-along--bootcamp.zip) and follow along.

## Exercises

Getting comfortable with the positioning and display properties will help you solve common layout issues. Download [positioningAndFloats.zip](https://hychalknotes.s3.amazonaws.com/positionAndFloats.zip) to help you practice the following concepts:

* floats
* relative and absolute positioning
* widths and heights
* CSS3 border radius
* Using `box-sizing:border-box;`
* z-index
* RGBA colours
* display inline, block and inline-block

There are six exercises, labelled `ex1` to `ex6`.

## More exercises

* Test your knowledge with this bonus challenge. Recreate Glossier's featured product section! You can download these files to get started: [glossier-featured-section.zip](https://hychalknotes.s3.amazonaws.com/glossier-featured-section.zip).

* Download [poolPartyFloatsExercise.zip](https://hychalknotes.s3.amazonaws.com/poolPartyFloatsExercise.zip) for more practice with floats. Open the answer file in your browser and try to match it!
