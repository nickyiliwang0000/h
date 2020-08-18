<!-- Student takeaway -->
<!-- By the end of this lesson, the student should be able to:
- Make a percentage-based layout with pixel margins using a .wrapper and calc()
- Understand the difference between vh and vw
- Explain what is not part of the measurement of vh (URL bar)
-->

# Advanced layouts

## Percentage-based layout

When using floats to layout a page, we need to ensure that the sum of the widths of floated elements is less than or equal to the width of the parent container so that the children can sit next to each other.

If the parent's width is, say, 800px, the children's widths can't add up to more than 800px, otherwise, the children will break on to separate lines. Add in some border or margin and this math can get tedious. Instead of using exact pixel values for our floated child elements, let's use percentages.


### Container elements

You'll notice that in many of our layout examples and exercises, we have a surrounding element that acts as a parent to the floated elements. This element has a common set of CSS properties applied: `max-width`, `width`, and `margin: 0 auto;`.

The `max-width` is a pixel width that refers to the maximum width the container will take up on the page, and will not be able to grow anymore. `Width` tells the content inside to take up a certain percentage of the wrapper's width. We can either set the width to be 100% of the wrapper or set it to be less if we want to create some padding between the content and the wrapper's edge. And finally, `margin: 0 auto` centers the wrapper and its contents for us.

We've usually given this element a class of `.wrapper` or `.container`, but these are arbitrary names. The wrapper element serves as a way to constrain our content while allowing the body to cover the entire browser window. This creates clean lines on our page and prevents content from being stretched out on very wide screen sizes.

![](https://hychalknotes.s3.amazonaws.com/fullbleed-design-wrapper--conEd.png)

The CSS for this page may look something like this 
```css
.wrapper {
  width:90%;
  margin: 0 auto;
  max-width:1200px;
}
```

If we don't have a wrapper, `width: 50%;` of the child element will be 50% of the browser window. This can get messy because there are many different device sizes available. 50% of a full-screen window on a 14" Acer Swift is different than 50% of a full-screen window on a 27" iMac Pro. And what happens when a user scales their browser? That size changes again! But if we use a wrapper, the child element will be only 50% of the width of the wrapper, not the whole browser window!

When working with percentages, it's important to think beyond the dimensions of your own devices. Remember that **100% is a relative value.**

```html
<div class="wrapper">
  <section></section>
  <aside></aside>
</div>
```

```css
.wrapper {
  max-width: 1280px;
  width: 100%;
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

If we've set a width on our wrapper to 1280px, what happens when the viewport is less than 1280px wide? The browser will still render an element that is 1280px with scroll bars to see the hidden parts of it.

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

In previous examples, we had to ensure that the widths of child elements added up to the same width of the parent container even when we wewere not using percentages:

```html
<main>
  <section></section>
  <aside></aside>
</main>

<style>
  main {
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
<main>
  <section></section>
  <aside></aside>
</main>

<style>
  main {
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

If we were using percentages, we could easily change the units of the margin to match, but 10% of a container is quite a lot for a margin.

```html
<main>
  <section></section>
  <aside></aside>
</main>

<style>
  main {
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
<main>
  <section></section>
  <aside></aside>
</main>

<style>
  main {
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

Percentages are relative values. Because we're using a fluid layout, we want the browser to recalculate the math every time we resize the browser window.

### CSS calculations

Luckily there is a CSS tool that allows us to resize elements accordingly. `calc()` does our math for us. We provide `calc()` as a value for a property and pass in the equation we want to be evaluated between the parentheses.

```css
section {
  width: calc(65% - 20px);
}
```

> Note that calc() is whitespace sensitive, so `calc(65%-20px)` will not work. Make sure to add spaces: `calc(65% - 20px)`.

Currently, `calc()` is almost universally supported across browsers and it is an essential property in the CSS toolkit. [To see the current support of calc() click here](<https://caniuse.com/#search=calc()>).

Using `calc()`, we can now mix percentages and pixels to create a layout that is fluid and looks great.

```html
<main>
  <section></section>
  <aside></aside>
</main>

<style>
  main {
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

![mathdog](http://i.giphy.com/UKkes2qN2T70s.gif)

### Resources

* Check out[ this great article on calc()](https://medium.com/@rbnhmll/love-in-the-time-of-calc-cc40142e4566) from HY Instructor Robin Hamill.
* To practice using floats and `calc()`, [watch this code-along video](https://youtu.be/HLftFGd_GrY) where Jenny will be using `calc()` to create a 3x3 gallery layout.


## Full bleed code-along

Download [fullbleed-layout-starter--bootcamp.zip](https://hychalknotes.s3.amazonaws.com/fullbleed-layout-starter--bootcamp.zip) and we can get practice combining all of these concepts to create a modern-looking website. 
