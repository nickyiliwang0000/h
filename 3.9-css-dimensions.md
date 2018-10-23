## Width and Height

Let's start things off and work with `width` and `height` to size our elements. Let's make a quick HTML document with four divs. 

```html
<div class="box1"></div>
<div class="box2"></div>
<div class="box3"></div>
<div class="box4"></div>
```

And then add a little CSS to style each box:

```css
.box1 {
	background:red;
}
.box2 {
	background:blue;
}
.box3 {
	background:green;
}
.box4 {
	background:orange;
}
```

So what does this look like so far? Nothing! Because there is no content, there is no width and no height in our boxes. They aren't taking up any room. We can change that by adding some content to each box:

```html
<div class="box1">Box #1</div>
<div class="box2">Box #2</div>
<div class="box3">Box #3</div>
<div class="box4">Box #4</div>
```

**Note:** in a normal document you should never put text inside a div without first wrapping it in a tag (such as `<p>` tags`</p>`) but we are leaving them out for simplicity :)

#### Auto Width

 You'll notice that the divs extend the **entire width** of the browser while the text is only a few characters long. Why? This is because **divs are block elements and have a width of auto** by default

#### Specifying Width and Height

Lets try a few different ways of specifying width and height:

```css
.box1 {
	background:red;
	width: 200px;
	height:200px;
}
.box2 {
	background:blue;
	width:100%;
	height:90px;
}
.box3 {
	background:green;
	width:2000px;
	height:150px;
}
.box4 {
	background:orange;
	width:500px;
	height:100%;
}
```

Produces the following:

![](http://wes.io/JGk7/Screen%20Shot%202012-09-06%20at%2011.46.52%20AM.png)

1. Box 1 is 200px by 200px - makes sense, right?
2. Box 2 is spanning 100% of the browser and 90px high - good!
3. Box 3 is 150px high and 2000px wide - much wider than my screen so we have to scroll right to see the entire box.
4. Box 4 is 500px wide - good - and 100% height - **Woah, hold on**. Why isn't box 4 taking up the rest of the room in the browser?

If 100% width takes up the entire width of the browser, shouldn't 100% height take up the entire height? That would make sense, but this is one of the many quirks of CSS. Giving an element 100% height means it will take up 100% of its _own_ content height - not the browser's height. As a proof of concept, lets add a **box 5** inside box 4 and give it a width and height of 150px;

![](http://wes.io/JGxM/Screen%20Shot%202012-09-06%20at%2011.58.58%20AM.png)

Because its child **Box 5** is 150px high, **Box 4** reacts and changes its height to 150px + the height of the text 'Box #4'.


## Padding and Margin

Along with your pals `width` and `height`, two of your CSS best friends will be `padding` and `margin`.

These two properties do what you might think - provide space between elements on your page so everything isn't squished together.

The only difference between the two is that margin adds space on the **outside** of an element while padding adds space on the **inside** of the element. It can be tough to remember so this little saying might help: "**Padding** protects your **insides**".

#### Giving it a shot
Let's give it a shot with some real markup. Start off with three basic divs:
```html
	<div class="box1">Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis.</div>
	<div class="box2">Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis.</div>
	<div class="box3">Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis.</div>
```

And some styling:

```css
.box1 {
	background:red;
}
.box2 {
	background:blue;
}
.box3 {
	background:green;
}
```

No big surprises here:

![](http://wes.io/JH4L/Screen%20Shot%202012-09-06%20at%202.08.04%20PM.png)

Go ahead and add some margin to box1, padding to box2 and both to box3:

```css
.box1 {
	background:red;
	margin:20px;
}
.box2 {
	background:blue;
	padding:20px;
}
.box3 {
	background:green;
	padding:20px;
	margin:20px;
}
```

![](http://wes.io/JHf6/Screen%20Shot%202012-09-06%20at%202.10.52%20PM.png)

1. Box 1 has 20px of margin outside the red, but the text is still squished inside the box.
2. Box 2 has 20px of padding inside the blue, but it's right up against the side of the browser.
3. Box 3 has both, allowing for enough space between both the text and the blue element above it.

#### One step further

In the last examples, we supplied a single value of 20px. What if we want to add margin/padding just to one side? We can append `-[side]` to the property.

```css
.box1 {
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
.box1 {
    margin: 10px 5% 10px 25px;
    padding: 10px 20px 25px 5%;
}
```

The order of the above is top, right, bottom and left. You can remember it easily because it's the same direction as a compass or a clock - or if you prefer, think of "trouble" - TRBL  (top, right bottom, left).

You may also set the top and bottom and right and left at the same time with the two number syntax:

```css
.box1 {
    margin:10px 20px; /* renders the same as 10px 20px 10px 20px */
}
```
Occasionally you will see three numbers which sets left and right with a single value. This is confusing and doesn't save much typing.

```css
.box1 {
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
.box1 {
    border-width:10px;
    border-color:red;
    border-style:solid;
}
```

If we don't specify a color, what happens? The color is inherited.

Width and color are pretty self explanatory. The **border style** allows you to set various styles of borders:

<div style="border:10px solid #D12026; margin:5px;">solid</div>
<div style="border:10px dotted #D12026; margin:5px;">dotted</div>
<div style="border:10px dashed #D12026; margin:5px;">dashed</div>
<div style="border:10px groove #D12026; margin:5px;">groove</div>
<div style="border:10px ridge #D12026; margin:5px;">ridge</div>
<div style="border:10px inset #D12026; margin:5px;">inset</div>
<div style="border:10px outset #D12026; margin:5px;">outset</div>

#### Targeting Single Sides
Just like padding and margin, we can target a single side to add a border. Just add the side like so:

```css
.box1 {
    border-[side]-width: 10px;
    border-[side]-color: red;
    border-[side]-style: solid;
}
```

#### Common Shorthand
You will frequently want to create a border that is the same `width`, `style` and `color` all the way around your element. If this is the case, you can use the border property and feed it each value separated by a space:

```css
.box1 {
    border:3px dotted red; /* [width] [style] [color] Much more sane */
}
```

#### Exercise

It's time to get comfortable with margin, padding, widths and borders, as well as to brush up on selectors.

Download <a href="https://hychalknotes.s3.amazonaws.com/3.9-CSSdimensions.zip" class="exercise" download>3.9-CSSdimensions.zip</a> and open 3.9-CSSdimensionsExercise.html in your editor and browser. You will find a set of instructions in the document.
Open 3.9-CSSdimensionsExercise-ANSWER.html in your browser to see what you are working towards.


## Border-Radius

Everything in HTML is a rectangle and has corners. However, a design may call for softer edges. This is where the border-radius property comes in handy, you can round the corners of an element while the element's 'footprint' still takes remains a rectangle.

Open up <a href="https://hychalknotes.s3.amazonaws.com/border-radius.html" class="exercise" download>border-radius.html</a> in the browser and editor and we can take a look at how it works.

Basic usage is to supply one value for all corners:

```css
.box1 {
    background: red;
    border-radius: 5px;
}
```

But we can also use short hand to specify TRBL (top, right, bottom, left):

```css
.box3 {
    background:blue;
    border-radius:5px 10px 100px 1px;
}
```
A 50% border radius makes a perfect circle. Go ahead and try some out.

You can even do it on an image:

```css
img.dog {
    border-radius: 50%;
}
```


## Border-Box

Now that we are equipped with width, height, padding, margin and borders, it's important to learn about the **box model**.

Create a new HTML file, and let's start off with a simple 150px by 150px box (set with `width` and `height`):

<div style="width:150px;height:150px;margin-bottom:30px;background:#ED9194;color:#000;font-weight:bold;letter-spacing:0.3px;box-sizing:content-box;">I'm a 150px by 150px box!</div>

Now let's add some padding so the text isn't all squished to the edge of the box.

<div style="width:150px;height:150px;margin-bottom:30px; background:#ED9194;padding:20px;color:#000;font-weight:bold;letter-spacing:0.3px;box-sizing:content-box;">I'm a 150px by 150px box with 20px of padding!</div>

Finally, add a border:

<div style="width:150px;height:150px;margin-bottom:30px; background:#ED9194;padding:20px;color:#000;font-weight:bold;letter-spacing:0.3px; border:10px solid black;box-sizing:content-box;">I'm a 150px by 150px box with 20px of padding and a 10px black border!</div>

Notice anything weird? The boxes grow as we add **padding** and **border**. Suddenly our 150px box isn't 150px anymore!

If the width and height of the box is set to 150px, why does the box get bigger? Why doesn't the padding and border take away from the 150 pixels? This is another CSS quirk that is quite an annoyance in web development. By default, `padding` and `border` changes the element's total size and `margin` adds to how much space the element is taking up. This interaction is referred to as **The Box Model**.

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

Similar to text-shadow, we also have box-shadow available to us which allows for adding shadow to the box around text as well as all other elements (such as divs, elements).

Take a look at <a href="https://hychalknotes.s3.amazonaws.com/box-shadow.html" class="exercise" download>box-shadow.html</a> for two examples on how to use box shadow - you'll notice its exactly the same syntax as text-shadow.

```css
.shadow {
  -moz-box-shadow:    3px 3px 5px 6px #ccc;
  -webkit-box-shadow: 3px 3px 5px 6px #ccc;
  box-shadow:         3px 3px 5px 6px #ccc;
}
```

1. The horizontal offset of the shadow, positive means the shadow will be on the right of the box, a negative offset will put the shadow on the left of the box.
2. The vertical offset of the shadow, a negative one means the box-shadow will be above the box, a positive one means the shadow will be below the box.
3. The blur radius (optional), if set to 0 the shadow will be sharp, the higher the number, the more blurred it will be.
4. The spread radius (optional), positive values increase the size of the shadow, negative values decrease the size. Default is 0 (the shadow is same size as blur).
5. Color.

<div style="width:100px;height:100px; background:#D12026;padding:10px;margin-bottom:15px;box-sizing:content-box;box-shadow: 5px 5px 5px #666;-moz-box-shadow: 5px 5px 5px #666;-webkit-box-shadow: 5px 5px 5px #666;">Box-Shadow</div>


**For some great examples of taking pure text to the next level, take a look at the examples at [http://tympanus.net/Tutorials/TypographyStyles/index4.html](http://tympanus.net/Tutorials/TypographyStyles/index4.html)**

![](http://wes.io/JPhe/Screen%20Shot%202012-09-12%20at%201.20.12%20PM.png)