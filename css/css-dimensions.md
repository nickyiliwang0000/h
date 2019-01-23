# CSS dimensions

## Width and Height

Let's start things off and work with `width` and `height` to size our elements. Let's make a quick HTML document with four divs. 

```html
<div class="container1"></div>
<div class="container2"></div>
<div class="container3"></div>
<div class="container4"></div>
```

And then add a little CSS to style each container:

```css
.container1 {
  background:#791313;
}
.container2 {
  background:#23395B;
}
.container3 {
  background:#3E5641;
}
.container4 {
  background:#FFBA08;
}
```

So what does this look like so far? Nothing! Because there is no content, there is no width and no height in our container. They aren't taking up any room. We can change that by adding some content to each container:

```html
<div class="container1">container #1</div>
<div class="container2">container #2</div>
<div class="container3">container #3</div>
<div class="container4">container #4</div>
```

**Note:** in a normal document you should never put text inside a div without first wrapping it in a tag (such as `<p>` tags`</p>`) but we are leaving them out for simplicity :)

#### Auto Width

 You'll notice that the divs extend the **entire width** of the browser while the text is only a few characters long. Why? This is because **divs are block elements and have a width of auto** by default

#### Specifying Width and Height

Lets try a few different ways of specifying width and height:

```css
.container1 {
  background:#791313;
  width: 200px;
  height:200px;
}
.container2 {
  background:#23395B;
  width:100%;
  height:90px;
}
.container3 {
  background:#3E5641;
  width:2000px;
  height:150px;
}
.container4 {
  background:#FFBA08;
  width:500px;
  height:100%;
}
```

Produces the following:

![A screenshot with four HTML elements, all with different dimensions.](https://hychalknotes.s3.amazonaws.com/css-dimensions-example1.png)

1. Container 1 is 200px by 200px - makes sense, right?
2. Container 2 is spanning 100% of the browser and 90px high - good!
3. Container 3 is 150px high and 2000px wide - much wider than my screen so we have to scroll right to see the entire box.
4. Container 4 is 500px wide - good - and 100% height - **Woah, hold on**. Why isn't container 4 taking up the rest of the room in the browser?

If 100% width takes up the entire width of the browser, shouldn't 100% height take up the entire height? That would make sense, but this is one of the many quirks of CSS. Giving an element 100% height means it will take up 100% of its _own_ content height - not the browser's height. As a proof of concept, lets add a **container 5** inside container 4 and give it a width and height of 150px;

![A screenshot of a nested HTML element with a height of 100%, illustrating how elements accept a height declaration in css.](https://hychalknotes.s3.amazonaws.com/css-dimensions-example2.png)

Because its child **container 5** is 150px high, **container 4** reacts and changes its height to 150px + the height of the text 'container #4'.


## Padding and Margin

Along with your pals `width` and `height`, two of your CSS best friends will be `padding` and `margin`.

These two properties do what you might think - provide space between elements on your page so everything isn't squished together.

The only difference between the two is that margin adds space on the **outside** of an element while padding adds space on the **inside** of the element. It can be tough to remember so this little saying might help: "**Padding** protects your **insides**".

#### Giving it a shot
Let's give it a shot with some real markup. Start off with three basic divs:
```html
<div class="container1">Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis.</div>
<div class="container2">Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis.</div>
<div class="container3">Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis.</div>
```

And some styling:

```css
.container1 {
  background:#3E5641; /* Green */
}
.container2 {
  background:#FFBA08; /* Yellow */
}
.container3 {
  background:#791313; /* Red */
}
```

No big surprises here:

![A screenshot of text inside of three HTML elements all very close together; the text is hugging the walls of the element because no padding or margin has been applied. ](https://hychalknotes.s3.amazonaws.com/css-dimensions-example3.png)

Go ahead and add some margin to container1, padding to container2 and both to container3:

```css
.container1 {
  background:#3E5641; /* Green */
  margin:20px;
}
.container2 {
  background:#FFBA08; /* Yellow */
  padding:20px;
}
.container3 {
  background:#791313; /* Red */
  padding:20px;
  margin:20px;
}
```

![A screenshot of three HTML elements with text inside. There is space between the elements and some space inside of the elements walls and the text illustrating the use of padding and margin.](https://hychalknotes.s3.amazonaws.com/css-dimensions-example4.png)

1. Container 1 has 20px of margin outside the red, but the text is still squished inside.
2. Container 2 has 20px of padding inside the blue, but it's right up against the side of the browser.
3. Container 3 has both, allowing for enough space between both the text and the blue element above it.

#### One step further

In the last examples, we supplied a single value of 20px. What if we want to add margin/padding just to one side? We can append `-[side]` to the property.

```css
.container1 {
	/* Specific margin values */
  margin-top: 10px;
  margin-right: 5%;
  margin-bottom:10px;
  margin-left: 25px;
	
	/* Same goes for padding */
  padding-top:10px;
  padding-right:20px;
  padding-bottom:25px;
  padding-left:5%;
}
```

#### That's too much typing! - CSS Shorthand

8 lines just for padding and margin? Seems like a lot of typing! Luckily we have a CSS shorthand for specifying padding and margin values (among other properties which we will learn about later). We can just supply the four values with spaces in between:
```css
.container1 {
  margin: 10px 5% 10px 25px;
  padding: 10px 20px 25px 5%;
}
```

The order of the above is top, right, bottom and left. You can remember it easily because it's the same direction as a compass or a clock - or if you prefer, think of "trouble" - TRBL  (top, right bottom, left).

You may also set the top and bottom and right and left at the same time with the two number syntax:

```css
.container1 {
  margin:10px 20px; /* renders the same as 10px 20px 10px 20px */
}
```
Occasionally you will see three numbers which sets left and right with a single value. This is confusing and doesn't save much typing.

```css
.container1 {
  margin:10px 20px 50px; /* renders the same as 10px 20px 50px 20px */
}
```

#### Centring elements with margins

Often we will want to center our website on a page. Since CSS doesn't have a center property for elements, we just use auto margins on the left and right to do this.

```css
.wrapper {
  margin:0 auto;
}
```

This will set the top and bottom margins to zero (you could set it to anything you want) and then the left and right to auto, which centers the element within the browser.


## Borders

Borders work similarly to padding and margin, but we use three properties instead of one. These properties are `border-width`, `border-color` and `border-style`.

```css
.container1 {
  border-width:10px;
  border-color:lightcoral;
  border-style:solid;
}
```

If we don't specify a color, what happens? The color is inherited.

Width and color are pretty self explanatory. The **border style** allows you to set various styles of borders. Let's open <a href="https://hychalknotes.s3.amazonaws.com/css-borders.html" class="exercise" download>css-borders.html</a> to take a look at some border styles.


#### Targeting Single Sides
Just like padding and margin, we can target a single side to add a border. Just add the side like so:

```css
.container1 {
  border-[side]-width: 10px;
  border-[side]-color: lightcoral;
  border-[side]-style: solid;
}
```

#### Common Shorthand
You will frequently want to create a border that is the same `width`, `style` and `color` all the way around your element. If this is the case, you can use the border property and feed it each value separated by a space:

```css
.container1 {
  border:3px dotted lightcoral; /* [width] [style] [color] Much more sane */
}
```

#### Exercise

It's time to get comfortable with margin, padding, widths and borders, as well as to brush up on selectors.

Download <a href="https://hychalknotes.s3.amazonaws.com/css-dimensions-exercise.zip" class="exercise" download>css-dimensions-exercise.zip</a> and open css-dimensions-exercise.html in your editor and browser. You will find a set of instructions in the document.
Open css-dimensions-exercise-ANSWER.html in your browser to see what you are working towards.


## Border-Radius

Everything in HTML is a rectangle and has corners. However, a design may call for softer edges. This is where the border-radius property comes in handy, you can round the corners of an element while the element's 'footprint' still takes remains a rectangle.

Open up <a href="https://hychalknotes.s3.amazonaws.com/css-border-radius.html" class="exercise" download>css-border-radius.html</a> in the browser and editor and we can take a look at how it works.

Basic usage is to supply one value for all corners:

```css
.container1 {
  background: #F08080;/* lightcoral */
  border-radius: 5px;
}
```

But we can also use short hand to specify TRBL (top, right, bottom, left):

```css
.container3 {
  background: #FFBA08; /* yellow */
  border-radius:5px 10px 100px 1px;
}
```
A 50% border radius makes a perfect circle. Go ahead and try some out.

You can even do it on an image:

```css
img.cat {
  border-radius: 50%;
}
```


## Border-Box

Now that we are equipped with width, height, padding, margin and borders, it's important to learn about the **box model**.

Create a new HTML file, and let's start off with a simple 150px by 150px container (set with `width` and `height`). Feel free to copy this element:

```html
<div>I'm a 150px by 150px container!</div>
```

Let's also open an internal stylesheet, and paste the following css:

```css 
div {
  width: 150px;
  height: 150px;
  background: #23395B;
  box-sizing: content-box;
  color: white;
}
```

Now let's add some padding so the text isn't all squished to the edge of the box.

```css 
div {
  width: 150px;
  height: 150px;
  background: #23395B;
  box-sizing: content-box;
  color: white;
  padding: 20px;
}
```

Finally, add a border:

```css 
div {
  width: 150px;
  height: 150px;
  background: #23395B;
  box-sizing: content-box;
  color: white;
  padding: 20px;
  border: 10px solid black;
}
```

Notice anything weird? The elements grow as we add **padding** and **border**. Suddenly our 150px container isn't 150px anymore!

If the width and height of the container is set to 150px, why does the element get bigger? Why doesn't the padding and border take away from the 150 pixels? This is another CSS quirk that is quite an annoyance in web development. By default, `padding` and `border` changes the element's total size and `margin` adds to how much space the element is taking up. This interaction is referred to as **The Box Model**.

If your project is only going to support Internet Explorer 8 and up, then we can use the `box-sizing` property like so: 

```css
* {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
```

By specifying this rule at the top of our CSS, we tell **all** elements (using the wildcard `*` selector) to take **padding** and **border** away from the set width and height. Grab the code from above and add it into your document.


## Box-Shadow

Similar to text-shadow, we also have box-shadow available to us which allows for adding shadow to the element around text as well as all other elements (such as divs, elements).

Take a look at <a href="https://hychalknotes.s3.amazonaws.com/css-box-shadow.html" class="exercise" download>css-box-shadow.html</a> for two examples on how to use box-shadow - you'll notice its exactly the same syntax as text-shadow.

```css
.shadow {
  -moz-box-shadow:    3px 3px 5px 6px #ccc;
  -webkit-box-shadow: 3px 3px 5px 6px #ccc;
  box-shadow:         3px 3px 5px 6px #ccc;
}
```

1. The horizontal offset of the shadow, a positive value means the shadow will be on the right of the element, a negative offset will put the shadow on the left of the element.
2. The vertical offset of the shadow, a negative value means the box-shadow will be above the element, a positive one means the shadow will be below the element.
3. The blur radius (optional), if set to 0 the shadow will be sharp, the higher the number, the more blurred it will be.
4. The spread radius (optional), positive values increase the size of the shadow, negative values decrease the size. Default is 0 (the shadow is same size as blur).
5. Color.