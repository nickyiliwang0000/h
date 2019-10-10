<!-- Student takeaway: -->
<!-- At the end of the lesson, the student will:
- Be able to explain the box model
- Know which snippet solves the box-model problem (box-sizing: border-box)
- Know about `float`
- Know which snippet solves the parent collapse issue created by floating (clearfix / group:after)
- Know which snippet normalizes browser defaults
 -->
# CSS layout

What makes a site easy to use? How should our content sit on the page? What happens when the viewport changes? These are questions you should ask yourself when you're thinking about your site's layout.

## Identifying structure

Every element in HTML exists as a box. Elements have dimensions (e.g. width and height) and can contain content or other elements.

We've already looked at grouping content using the `<div>` tag and/or semantic elements, for readability and accessibility. On top of that though, we also group content in anticipation of the styling we'll apply to it.

In HTML, almost all structural elements take up 100% of the width of the browser.  These elements are known as _block elements_. All elements render in the browser in the order they appear in the HTML markup; kind of the way a word processor works.

Check out [this CodePen](https://codepen.io/hackeryou/pen/yQeXQO) for a quick visual refresher on block elements, or copy-paste the following code into a file of your own:

```css
section{
  background-color:aqua;
  height: 100px;
}
aside{
  background-color: lavender;
  height: 50px;
}
```

```html
<div class="container">
  <section>
    <h2>This is a section</h2>
  </section>
  <aside>
    <h3>This is an aside</h3>
  </aside>
</div>
```

## Adding dimensions

Every website you've ever seen isn't just stuff stacked up in the browser. There are articles next to sidebars, footers that span a whole page, and masonry layouts. Lists, especially navigations, can run inline rather than stack up.

It makes sense to assume that since all block elements default to a width of 100% of the browser window, changing the elements' width to 50% should allow two elements to sit next to each other.

Go back to [this CodePen](https://codepen.io/hackeryou/pen/yQeXQO) and add `width: 50%;` to the block elements, like so:

```css
section{
  background-color:aqua;
  height: 100px;
  width:50%;
}
aside{
  background-color: lavender;
  height: 50px;
  width:50%;
}
```

```html
<div class="container">
  <section>
    <h2>This is a section</h2>
  </section>
  <aside>
    <h3>This is an aside</h3>
  </aside>
</div>
```

Why isn't the aside coming up to sit by the section?!

![diagram showing how block elements are expected sit on a line together at 50% width each](https://hychalknotes.s3.amazonaws.com/expected-block-behavior.png)

This is one of the weird things about HTML/CSS layout. Block elements **always** always take up a 100% of the browser window regardless of their declared/rendered width. Weeeeeiiiiirrrddddddd!

## The `float` property

The early developers of HTML and CSS did not plan for the kind of web page layouts we're used to, but they **did** plan for text to wrap around images, like it does in books and magazines. The `float` property can be applied to images to define how the following elements will wrap around them.

Check out [this CodePen](https://codepen.io/hackeryou/pen/qQbXez) to see the paragraph text wrapping around the image, or copy-paste the following code into a file of your own:

```css
  img{
    float:left;
  }
```
```html
<img src="http://unsplash.it/200/200" alt="image from unsplash">
<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Nobis qui veritatis saepe cum corrupti ex quibusdam, magni quas autem, deserunt sint alias. At et, sed veniam, beatae porro animi qui.</p>
<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Nobis qui veritatis saepe cum corrupti ex quibusdam, magni quas autem, deserunt sint alias. At et, sed veniam, beatae porro animi qui.</p>
<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Nobis qui veritatis saepe cum corrupti ex quibusdam, magni quas autem, deserunt sint alias. At et, sed veniam, beatae porro animi qui.</p>
<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Nobis qui veritatis saepe cum corrupti ex quibusdam, magni quas autem, deserunt sint alias. At et, sed veniam, beatae porro animi qui.</p>
```

Change the value for `float` to `right`, then to `none`, then back to `left` to see how the image moves within its parent and how the rest of the content wraps around it.

## Exercise: Floating images
Open up [image-float.html](https://hychalknotes.s3.amazonaws.com/floating-image.html) in your text editor and the browser. If you get stuck, check out the answer [here](https://hychalknotes.s3.amazonaws.com/floating-imageANSWER.html).

## Using floats for layout
We can use floats to help lay out our structural elements, not just our images. If we think of each row/line as 100%, we need to ensure that the sum of all the elements' dimensions in any given row are equal to or less than 100%. Anything that doesn't fit into that space gets moved to the next line.

All structural elements are block elements, which means they're how wide by default?
<!-- They take up 100% of the width of the browser window -->
> 100% of the width of the browser window!

Go back to [this CodePen](https://codepen.io/hackeryou/pen/yQeXQO) and add `float: left;` to the block elements, like so:

```css
section{
  background-color:aqua;
  height: 100px;
  width:50%;
  float:left;
}
aside{
  background-color: lavender;
  height: 50px;
  width:50%;
  float:left;
}
```

```html
<div class="container">
  <section>
    <h2>This is a section</h2>
  </section>
  <aside>
    <h3>This is an aside</h3>
  </aside>
</div>
```
Remove the `width:50%;` on both elements. What happens?

You'll see that when you apply a `float` to an element, that element's width becomes the size of its contents unless otherwise specified.

## Floated elements' stacking order

When elements are floated, their _stacking order_ will also change. Stacking order is the way elements appear on the page. When you float an element, you're essentially lifting it out of the flow of the page and letting it float above its surrounding element. The floated element will also lose its imprint and and its space won't be saved. Often, you will find the surrounding elements shuffling into the space that the floated element used to take up. [Here is a great video](https://www.youtube.com/watch?v=xara4Z1b18I) that explains how floating elements affect their stacking order.

You can kind of think of it like people in line at the cash at the grocery store: you get into line in the order you finish shopping (natural stacking order). If you leave the line to go to the self-checkout (float), the people who were behind you will fill your spot. If the self-checkout is broken, hopefully people will let you back in line in your original spot. (A floated element always takes its original position back when the float is removed. A web page is like like a very polite community of shoppers.)

Check out [this CodePen](https://codepen.io/jenobot/pen/QOzyeP/) to see how stacking order changes when an element is floated.

<!-- ## Calculating dimensions

Before we move on, we need to understand how we use margin, padding and borders in layouts. A brief review of those properties:

property | used to |
---|---
`margin` |  push elements away from each other
`padding` | push content away from the inside walls of an element
`border` | surround an element and its padding

Check out [this CodePen](https://codepen.io/CoderOfNote/pen/gOOpEmr?editors=1100) and comment-in the margin, padding, and border on the first image.

See how the element is defined as 200px by 200px, but the padding makes the element larger?
![an image element with 50px of padding](https://hychalknotes.s3.amazonaws.com/box-model-padding.png)

And so does the border! 

![an image element with 50px of padding and 50px of border](https://hychalknotes.s3.amazonaws.com/box-model-border-padding.png)

So what we defined as a 200px square is now a 300px square! 

The 25px of margin that we added affects the element's footprint, not its actual size. With the margin applied, the element will take up `25px + 300px + 25px` of space in the browser window. 

This is what is known as the _box model_. A developer (or the content) defines an element's size and the padding and border are **added** to that size. This can be confusing, especially when we're using floats with these widths.

Download and open up [box-model-playground.html](https://hychalknotes.s3.amazonaws.com/box-model-playground.html) in your text editor and browser. Play around with the padding, border and margin of each box and see how it can affect their total dimensions.

## Border-box

The box model can be navigated around quite easily. By adding the following code to the top of your CSS file, we can make the padding and border **not** add to the computed size of our element.

```css
* {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
```

The `*` character is a wildcard selector and selects everything on the page.

When starting any project from now on, be sure to include that at the top of your CSS file. -->

## Two column layout

One familiar web page layout includes a `header` and a `footer`, and in between those, a content area with an `aside` next to it.

Open up <a href="https://hychalknotes.s3.amazonaws.com/column-layout.html" class="exercise" download>column-layout.html</a> to follow along.
 
In our example, we have our four main elements. `header`, `section`, `aside` and `footer`. We also have a surrounding element with a class of `wrapper` that constrains our elements and centers them.

```html
  <div class="wrapper">
      <header>
          <h1>Welcome To HackerYou</h1>
      </header>
      <section>
          <h2>This is the story of a girl.</h2>
          <p>Born and raised in Houston, Texas, Beyoncé performed in various singing and dancing competitions as a child. She rose to fame in the late 1990s as lead singer of the R&B girl-group Destiny's Child. Managed by her father Mathew Knowles, the group became one of the best-selling girl groups in history. Their hiatus saw Beyoncé's theatrical film debut in Austin Powers in Goldmember (2002) and the release of her first solo album, Dangerously in Love (2003). The album established her as a solo artist worldwide, debuting at number one on the US Billboard 200 chart and earning five Grammy Awards, and featured the Billboard Hot 100 number one singles "Crazy in Love" and "Baby Boy".</p>
      </section>
      <aside>
          <ul>
              <li>Clickbait Synergist</li>
              <li>Paradigm Optimization</li>
              <li>Bleeding Edge Exit Strategy</li>
          </ul>
      </aside>
      <footer>
          <p>Copyright 2018</p>
      </footer>
  </div>
```
By default, our elements are 100% wide, so we don't need to apply any widths or floats to our header or footer. However, we do want  `section` and `aside` next to each other. We'll use floats. Once the elements are floated, we'd like them to add up to 100% of the browser window width.

```css
section {
    float: left;
    width: 60%;
}

aside {
    float: left;
    width: 40%;
}
```

Great, the `section` and `aside` are next to each other, but our footer has jumped up and our wrapper  has collapsed.

![float collapse](https://hychalknotes.s3.amazonaws.com/column-layout-screenshot.png)

Weird! How do we fix these unexpected bugs?

## Float problems
### Collapse of surrounding element
Floats were created to allow text to wrap around an image and continue down the page. In the layout we're working with, we don't have enough content in the `aside` to continue down the page, so the wrapper sizes to the next element that isn't floated. In this case, the `footer` element.


#### Solution: `.clearfix`

The industry standard method of solving this problem is mostly referred to as `clearfix`. (The class name of `clearfix` is an industry standard, but it can be named whatever you'd like.) Along with the `border-box` fix, we recommend that you include the following code at the **top** of all our `styles.css` files moving forward.

```css
.clearfix:after {
  visibility: hidden;
  display: block;
  font-size: 0;
  content: " ";
  clear: both;
  height: 0;
} 
```
 Whenever you are floating an element, apply a class of `clearfix` to the **parent** element.

```html
<section>
  <div class="wrapper clearfix">
    <div class="half">
      <p>The div that contains this paragraph is floated left</p>
    </div>
    <div class="half">
      <p>The div that contains this paragraph is also floated left</p>
    </div>
  </div>
</section>
```


### Following elements are broken

When using floats, we can fix the elements that pop up after our floated elements by adding the rule `clear:both;` to their styles. Using `clear:both;` on the following, sibling element will stop the floating layout and return the element you target **and** all following elements to their original layout state.

```css
footer {
  clear: both;
}
```

## Removing browser default styles

All browsers come with style defaults, such as making all `h1`-`h6` elements escalate in size and adding padding and margins to various elements. Though you may like some of the default styles, they aren't consistent across all browsers. This can lead to lots of debugging headaches. A CSS snippet referred to as `CSS normalize` or `CSS reset` strips out all the browser's default styles. We can either insert it at the top of our main CSS file or add as a separate stylesheet in the `<head>` of our HTML document.

If you add it as a separate stylesheet, **it should be included before your custom stylesheet**.

If you don't already have it as a snippet, you can download normalize.css at <http://necolas.github.com/normalize.css/>, or [find it here](https://hychalknotes.s3.amazonaws.com/normalize-v700.css). We won't be using it in our examples, but all of your projects should include it.

## Gallery layout exercises
Let's create a floated layout together together to start. Open up [gridLayout.html](https://hychalknotes.s3.amazonaws.com/gridLayout.html) in your text editor and in the browser. If you get stuck, check out [gridLayoutANSWER.html](https://hychalknotes.s3.amazonaws.com/gridLayoutANSWER.html).

Next, let's create a more complex layout in [clearBothExercise.zip](https://hychalknotes.s3.amazonaws.com/clearBothExercise.zip).

Open up [galleryLayoutExercise.zip](https://hychalknotes.s3.amazonaws.com/galleryLayoutExercise.zip) and let's work through an example of how to create a gallery style layout using floats. 
> Note that this exercise contains a gotcha! (Hint: the image sizes are different!) 

Try revisiting the two column layout: can you create it on your own? Download [advancedTwoColumn.zip](https://hychalknotes.s3.amazonaws.com/advancedTwoColumn.zip) and follow the instructions in the comments.

## More exercises
For extra practice, work on [structuralElements.html](https://hychalknotes.s3.amazonaws.com/structuralElements.html) and follow the instructions in the comments! If you get stuck [check out the answer here](https://hychalknotes.s3.amazonaws.com/structuralElementsAnswer.html).

For a pretty tough CHALLENGE, download this [pool party exercise](https://hychalknotes.s3.amazonaws.com/poolPartyFloatsExercise.zip)!