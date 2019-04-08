<!-- Student takeaway -->
<!-- By the end of this lesson, the student should be able to:
- Make a percentage-based layout with pixel margins using a .wrapper and calc()
- Understand the difference between vh and vw
- Explain what is not part of the measurement of vh (URL bar)
-->

# Advanced layouts

## Percentage-based layout

When using floats to lay out a page, we need to ensure that the sum of the widths of floated elements is less than or equal to the width of the parent container so that the children can sit next to each other.

If the parent's width is, say, 800px, the childrens' widths can't add up to more than 800px, otherwise the children will break on to separate lines. This math can get tedious, so instead of using exact pixel sizes for our floated child elements, let's use percentage values.

Open [advanced-layouts-starter.html](https://hychalknotes.s3.amazonaws.com/advanced-layouts-starter.html) and changes the pixels sizes of the floated child elements to percentages.

### Container elements

You'll notice that in all of our layout examples, we have a surrounding element that acts as our parent element. This element has a pixel size and `margin: 0 auto;` applied.

We've usually given this element a class of `.wrapper` (this is an arbitrary name). The wrapper serves as a way to constrain our content while allowing the body to cover the entire browser window.

If we don't have a wrapper, `width: 50%;` will be 50% of the browser window. This can get messy because there are many different device sizes available. 50% of a 14" Acer Swift is different than 50% of a 27" iMac Pro. And what happens when a user scales their browser? When working with percetages, it's important to think beyond the dimensions of your own devices. Remember that **100% is a relative value.**

```html
<div class="wrapper">
  <section></section>
  <aside></aside>
</div>
```

```css
.wrapper {
  width: 1280px;
  margin: 0 auto;
}

section {
  width: 65%;
  float: left;
}

aside {
  width: 35%;
  float: left;
}
```

In the above example, we can see that the `section` element is 65% of the parent element. Knowing that the parent element is 1280px, we can conclude that the section will render at 832px wide.

### `max-width`

If we've set a width on our wrapper to 1280px, what happens when the viewport is less than 1280px wide? The browser will still render an element that is 1280px wide and scroll bars to see the hidden parts of it.

To combat this problem, we can replace the `width` property on the wrapper with a `max-width` property.

```css
.wrapper {
  max-width: 1280px;
  margin: 0 auto;
}
```

`max-width` allows the element to resize for smaller devices. The element will be 100% of it's parent element **until** it reaches 1280px, and then it will stop growing.

The opposite of `max-width` is `min-width`, a property that specifies the smallest possible size for an element.

The corresponding `max-height` and `min-height` properties are less used but can be useful when working with dynamic content.

Moving forward, it's best practice to include a `max-width` property with a pixel value on your containing element (i.e. wrapper) when you use percentages for floated child elements.

## `calc()`

### Mixing pixels with percentages

Now that we understand how to limit the sizing and see the benefits of using percentages with our elements, what if we want to put some space between our elements?

Open up [calcLayout.html](https://hychalknotes.s3.amazonaws.com/calcLayout.html) to follow along.

In previous examples, we had to ensure that the widths of child elements added up to the same width of the parent container.

```html
<div class="wrapper">
  <section></section>
  <aside></aside>
</div>

<style>
  .wrapper {
    max-width: 800px;
  }

  section {
    float: left;
    width: 500px;
  }

  aside {
    float: left;
    width: 300px;
  }
</style>
```

However, if we used margin to provide spacing between our elements, we would have to account for it when setting the widths of our elements.

```html
<div class="wrapper">
  <section></section>
  <aside></aside>
</div>

<style>
  .wrapper {
    max-width: 800px;
  }

  section {
    float: left;
    width: 480px;
    margin: 0 10px;
  }

  aside {
    float: left;
    width: 280px;
    margin: 0 10px;
  }
</style>
```

If we were using percentages, we could easily change the units of the margin to match, but 10% of a container is quite a big size for a margin.

```html
<div class="wrapper">
  <section></section>
  <aside></aside>
</div>

<style>
  .wrapper {
    max-width: 800px;
  }

  section {
    float: left;
    width: 45%;
    margin: 0 10%;
  }

  aside {
    float: left;
    width: 15%;
    margin: 0 10%;
  }
</style>
```

So instead of working with unclear percentage margins, why don't we work with percentages for widths, and something more tangible for margins: pixels.

```html
<div class="wrapper">
  <section></section>
  <aside></aside>
</div>

<style>
  .wrapper {
    max-width: 800px;
  }

  section {
    float: left;
    width: 65%;
    margin: 0 10px;
  }

  aside {
    float: left;
    width: 35%;
    margin: 0 10px;
  }
</style>
```

So 10px + 10px = 20px. 65% - 20px = ?

This is where it gets tricky - percentages are relative values. Because we're using a fluid layout, we have to do the math every time we wanted to resize the screen.

### CSS calculations

Luckily there is a CSS tool that allows us to resize things accordingly. We can use `calc()`, which does the math for us. We provide `calc()` as a value for a property and pass in the equation we want to be evaluated between the parentheses.

```css
section {
  width: calc(65% - 20px);
}
```

> Note that calc() is whitespace sensitive, so `calc(65%-20px)` will not work.

Currently, `calc()` is pretty well supported across different browsers and will become part of our CSS toolkit moving forward. [To see the current support of calc() click here](https://caniuse.com/#search=calc()).

Using `calc()`, we can now mix percentages and pixels to create a layout that is fluid and looks great.

```html
<div class="wrapper">
  <section></section>
  <aside></aside>
</div>

<style>
  .wrapper {
    max-width: 800px;
  }

  section {
    float: left;
    width: calc(65% - 20px);
    margin: 0 10px;
  }

  aside {
    float: left;
    width: calc(35% - 20px);
    margin: 0 10px;
  }
</style>
```

Look at you go!
![A dog trying to carry a stick over a bridge, but the stick's too wide.](http://i.giphy.com/UKkes2qN2T70s.gif)

### Resources

* Check out[ this great article on calc()](https://medium.com/@rbnhmll/love-in-the-time-of-calc-cc40142e4566) from HY Instructor Robin Hamill.
* To practice using floats and `calc()`, [watch this code-along video](https://youtu.be/HLftFGd_GrY) where Jenny will be using `calc()` to create a 3x3 gallery layout.

## Using the viewport to size content

The _viewport_ is the current size of the viewable content area of your browser. The viewport does **not** include the address or bookmarks bar. It is the entire area within which HTML is rendered.

![browser viewport](https://hychalknotes.s3.amazonaws.com/viewport.png)

The size of the viewport is dynamic. Viewport width and height are relative values that can be different on every user's device and when the user drags the browser window.

Web experiences often feature full browser header images or content that is relative to the size of the user's browser. Imagine how difficult it would be to ensure that an element fit 100% of the viewport on every screen. In the past, we used JavaScript to measure the size of the window once all the content was loaded, and resize the elements accordingly.

We discussed other standard units found on the web in the [CSS measurement units](https://github.com/HackerYou/bootcamp-notes/blob/master/css/css-measurement-units.md) lesson, but there are a couple more recent additions to the dimension discussion. `vw` and `vh` units allow us to measure the user's viewport in CSS without the need for JavaScript. These units measure the width of the viewport and return a relative value. These units are [not fully supported in legacy browsers](http://caniuse.com/#search=view) but can be very handy.

### `vh`

`vh` measures viewport height. Think of it as a percentage - the full height of the viewport is 100%. This gets used mainly for large header images or initial load pages.
Remember, `vh` **does not** include the URL bar on mobile devices.

> 100% of the height of the viewport is `100vh`.

![Diagram of a browser showing where viewport height is measured](https://hychalknotes.s3.amazonaws.com/viewportVH.png)

### `vw`

`vw` is viewport width. You may find that you do not use it as often as other units.

![Diagram of a browser showing where viewport width is measured](https://hychalknotes.s3.amazonaws.com/viewportVW.png)

## Full bleed code-along

Download [fulbleed-codealong-bootcamp.zip](https://hychalknotes.s3.amazonaws.com/fulbleed-codealong-bootcamp.zip) and we'll see how `vh` can be used to create a modern-looking website.
