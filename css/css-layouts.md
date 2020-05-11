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

Check out [this CodePen](https://codepen.io/hackeryou/pen/yQeXQO) for a quick visual refresher on block elements:

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

### Adding dimensions

Most websites aren't just stuff stacked up in the browser. There are articles next to sidebars, footers that span a whole page, and masonry layouts. Lists, especially navigations, can run inline rather than stacking up.

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

Why isn't the aside coming up to sit by the section?!

![diagram showing how block elements are expected sit on a line together at 50% width each](https://hychalknotes.s3.amazonaws.com/expected-block-behavior.png)

This is one of the weird things about HTML/CSS layout; block elements always always stack vertically, regardless of their declared/rendered width.

There are a number of ways to use CSS to solve this limitation to page layout. The most common are Flexbox and CSS grid; both are great and will work for you on all projects you build going forward, but they are relatively recent additions to the CSS spec. Part of being a professional web developer is also being able to support common legacy technologies. Among the most prevalent of these, which you will likely run into frequently on the job, is what was previously the most common way to handle complex page layouts - _floats_.


## Floats

The early developers of HTML and CSS did not plan for the kind of web page layouts we're used to, but they did plan for text to wrap around images like it does in books and magazines. The `float` property can be applied to images to define how following elements will wrap around them.

Applying the `float` property to images defines how following elements will wrap around them. Check out [this CodePen](https://codepen.io/CoderOfNote/pen/BaajyJY?editors=1100#0) to see the paragraph text wrapping around the image. Change the value for `float` to `right`, then to `none`, then back to `left` to see how the image moves within its parent and how the rest of the content wraps around it.

### Exercise: Floating images
Open up [image-float.html](https://hychalknotes.s3.amazonaws.com/floating-image.html) in your text editor and the browser. If you get stuck, check out the answer [here](https://hychalknotes.s3.amazonaws.com/floating-imageANSWER.html).

### Using floats for layout

<!-- Rework this section to open with more of a "floats became a way to solve layout problems, even though they're not designed for that." Show the example with the first codepen below, but then explain that what's happening is that the element is being floated out of the flow of the page, so we need clearfix etc. -->

<!-- Also move thing about making sure row items equal or are less than 100% to after showing the codepen in action, since otherwise there's no context for what we're talking about (that the items are in a line) -->

Although floats were only designed to let text wrap around images, they were repurposed by developers to build layouts where elements sit beside one-another.

Go back to [this CodePen](https://codepen.io/hackeryou/pen/yQeXQO) and along with `width: 50%` add `float: left;` to the block elements, like so:

```css
section{
  background-color: aqua;
  height: 100px;
  width: 50%;
  float: left;
}
aside{
  background-color: lavender;
  height: 50px;
  width: 50%;
  float: left;
}
```

The two elements **float** up to sit beside one-another. They fit because we've set their widths to 50%. If the sum of all the elements' widths (plus any margins!) in any given row is more than 100%, then anything that doesn't fit gets moved to the next line. Try changing the width of the `aside` to 60% to see this happen.

On the other hand, what happens if we remove the `width` declaration from both elements? When you apply a `float` to an element, it no longer behaves as a block level element. Instead, its width becomes the size of its contents unless otherwise specified.

This seems great, we can lay out content horizontally. Again though, floats were never designed to build complex page layouts, and using them this way comes with its own complications that have to be accounted for.


### Floating elements' complicated behavior

When you float an element, you're essentially lifting it out of the normal flow of an HTML page; it floats up, out of its original position and to the front of its container. Its original footprint on the page disappears, which causes two major issues:

* Any following elements will move up to take the floated item's place in the DOM flow.
* The element's parent shrinks/collapses, since it no longer accounts for wrapping the floated element.


#### Stacking order

An element floating up out of the natural page flow and other elements taking its place means that the _stacking order_ of the HTML elements (the way they appear on the page) changes. [Here is a great video](https://www.youtube.com/watch?v=xara4Z1b18I) that explains how floating elements affect their stacking order.

You can kind of think of it like people in line to pay at the grocery store; you get into line in the order you finish shopping (natural stacking order), but if you leave the line to go to the self-checkout (float), the people who were behind you will fill your spot. If the self-checkout is broken, hopefully people will let you back in line in your original spot. A floated element always takes its original position back when the float is removed - a web page is like a very polite community of shoppers.

Check out [this CodePen](https://codepen.io/jenobot/pen/QOzyeP/) to see how stacking order changes when an element is floated.


#### Parent element collapse

When we float an element, its parent element no longer accounts for the floated elements' size, so the parent collapses. This causes all kinds of problems, since it means the floated elements will break out of their parent containers and overlap with following elements.

Lucky for us, floats became such a common tool for page layouts that a fairly standardized fix was developed and became commonplace. It is a CSS rule called _clearfix_, which we can apply to these parent elements. It makes them account for floated children, and go back to wrapping all their descendants. We will look at this in the following exercise.


### Two column layout

One familiar web page layout includes a `header` and a `footer`, and in between those, a content area with an `aside` next to it.

Open up <a href="https://hychalknotes.s3.amazonaws.com/column-layout.html" class="exercise" download>column-layout.html</a> to follow along.
 
In our example, we have our four main elements. `header`, `section`, `aside` and `footer`. We also have a surrounding element with a class of `wrapper` that constrains our elements and centers them.

```html
<div class="wrapper">
  <header>
    <h1>Welcome To Juno</h1>
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
    <p>&copy; Copyright 2049</p>
  </footer>
</div>
```

By default, our elements are 100% wide, so we don't need to apply any widths or floats to our header or footer. However, let's say we want `section` and `aside` next to each other. We can use floats. Once the elements are floated, we'd like them to add up to 100% of the browser window width.

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

Great, the `section` and `aside` are next to each other, but because they're no longer in the regular flow of our document, our `.wrapper` div has collapsed and the `footer` has jumped up to the top.

![float collapse](https://hychalknotes.s3.amazonaws.com/column-layout-screenshot.png)


#### `.clearfix`

To fix the collapsed wrapper, we can use the industry standard method we mentioned earlier, clearfix. To do this, we first define a class, `.clearfix`, at the top of our CSS:

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

Along with the `border-box` fix, you should include the above code at the top of your CSS files for any project you build with floats.

Next, you apply the clearfix class to the **parent** of any floated elements on your page:

```html
<section>
  <div class="wrapper clearfix">
    <!-- The div below is floated left! -->
    <div class="half">
      <p>The div that contains this paragraph is floated left</p>
    </div>

    <!-- The div below is also floated left! -->
    <div class="half">
      <p>The div that contains this paragraph is also floated left</p>
    </div>
  </div>
</section>
```

Note that while `.clearfix` is the most common standard, like any class name, we can name it anything we want. Other common names are `.clearfloat` and [`.group`](https://css-tricks.com/snippets/css/clear-fix/).

Let's add the clearfix CSS rule to our styles and apply the class to our wrapper div in the exercise. The wrapper now surrounds all our elements instead of collapsing.


#### Fixing the stacking order

Our `footer` is still up behind our `section` and `aside`, because while clearfix made our wrapper account for the floated elements, we still haven't told the `footer`, a sibling which follows our floated elements, to maintain the page's original stacking order.

To do this, we apply a `clear: both;` rule to our `footer`. This rule tells an element which follows floated items to clear itself of the floating layout, and to return itself and all following elements to their original layout:

```css
footer {
  clear: both;
}
```

Finally, our page looks the way we want!


## Removing browser default styles

All browsers come with style defaults, such as making all `h1` to `h6` elements be sizes largest to smallest, and adding padding and margins to various elements. Although you may like some of the default styles, they aren't consistent across all browsers ,which can lead to lots of debugging headaches. A CSS snippet referred to as `CSS normalize` or `CSS reset` strips out all the browser's default styles. We can either insert it at the top of our main CSS file or add as a separate stylesheet in the `<head>` of our HTML document.

If you add it as a separate stylesheet, it should be included before your custom stylesheet.

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
