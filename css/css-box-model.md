# CSS Box Model

**Every HTML element is a rectangular box.**
A website/project built with HTML and CSS is essentially just a page composed of boxes and boxes inside boxes. We use CSS to style those boxes into our desired layout and design.  

CSS Box Model is the term that describes the properties of the box. These properties are: 
- **Content**: content area of the box
- **Padding**: transparent spacing around the content area
- **Border**: border of the box
- **Margin**: transparent spacing area outside of the border

<img src="https://camo.githubusercontent.com/ff18f1d19dc865c72501cdab7c60b928b21c8eec/68747470733a2f2f68796368616c6b6e6f7465732e73332e616d617a6f6e6177732e636f6d2f626f782d6d6f64656c2d2d636f6e45642e6a7067" alt="css box model">

To explore these properties better, let's create a basic HTML document with 3 box divs in it:

```html
<div class="box1"></div>
<div class="box2"></div>
<div class="box3"></div>
```

And then add a background color to each box:

```css
.box1 {
  background-color: gold;
}
.box2 {
  background-color: paleturquoise;
}
.box3 {
  background-color: lightsalmon;
}
```

Why aren't we seeing anything on the page? 

## Width and height

Our boxes are currently empty boxes. **When an element has no content, it has no height.** In order to change this we can: 
- Provide our element with content or,
- Specifying height. 

Let's try to add some content into our boxes:

```html
<div class="box1">Box 1</div>
<div class="box2">Box 2</div>
<div class="box3">Box 3</div>
```

**Note:** in a normal document you should never put text inside a div without first wrapping it in a tag (such as `<p>` tags`</p>`) but we are leaving them out for simplicity :)

<img src="https://hychalknotes.s3.amazonaws.com/box-model-1.png" alt="screenshot of auto width">

Notice that the divs extend the **entire width** of the browser while the text is only a few characters long. This is because **divs are block elements**. Block elements will take up the entire width of the available space by default. We will talk more about block elements in another lesson. 

The default values for `width` and `height` properties are set to `auto`, which means they will automatically adjust themselves to the content. 

### Specifying width and height

To override the default, we can provide specific values to the `width` and `height` properties. 

```css
.box1 {
  background-color: gold;
  width: 200px;
  height: 200px;
}
.box2 {
  background-color: paleturquoise;
  width: 80%;
  height: 300px;
}
.box3 {
  background-color: lightsalmon;
  width: 3000px;
  height: 100%;
}
```

Produces the following:

<img src="https://hychalknotes.s3.amazonaws.com/box-model-2.png" alt="A screenshot with four HTML elements, all with different dimensions.">

1. Box 1 is 200px by 200px - makes sense!
2. Box 2 is spanning 80% of the browser width and 300px high - good!
3. Box 3 is 3000px width, much wider than our current screen size so we have to scroll right to see the entire box - cool.
**But Woah, hold on**, what's happening with the **100% height??**

### `width: 100%;` & `height: 100%;`

If 100% width takes up the entire width of the browser, shouldn't 100% height take up the entire height of the browser? That would make sense, but this is one of the many quirks of CSS. 

Whenever we set `100%` value to the `width` and `height` properties of an element, the element will be referring to **100% relative to the parent element**. 

In this case the parent element is the `<body>` element. The `<body>` element does not have a specified `height` value set, which means it is only as high as the space content will take up. 

You can try testing this out by setting a height value for the `<body>` element. 
```css
body {
  height: 500px; 
}
```

You will see now that box 3 has a height of 500px as it is set to be 100% of its parent element. 

## Padding and margin

Along with your pals `width` and `height`, two of your CSS best friends will be `padding` and `margin`.

These two properties do what you might think - provide space between elements on your page so everything isn't squished together.

Have a look at our box model diagram above. The difference between the two is that margin adds space on the **outside** of an element while padding adds space on the **inside** of the element. It can be tough to remember so this little saying might help: "**Padding** protects your **insides**".

Let's add some lorem ipsums to our boxes and remove the `height` and `width` values on our boxes. 

```html
<div class="box1">Lorem ipsum dolor sit amet consectetur, adipisicing elit. Fuga exercitationem nemo quod atque dignissimos ullam ex nisi consequuntur illum quam doloribus, dolor quisquam autem soluta cum tempore unde! Fuga, exercitationem.</div>
<div class="box2">Lorem ipsum dolor sit amet consectetur adipisicing elit. Voluptatum ut alias animi quibusdam, debitis doloremque eligendi vero ducimus voluptatem. Eligendi corporis quibusdam ullam autem veritatis iste sed recusandae nobis inventore!</div>
<div class="box3">Lorem ipsum, dolor sit amet consectetur adipisicing elit. Et dolor rem dolorum non ullam inventore porro esse, quibusdam dicta ipsa omnis qui placeat itaque illo, corporis ducimus distinctio voluptate nesciunt.</div>
```
Your page should now look like this:

![A screenshot of text inside of three HTML elements all very close together; the text is hugging the walls of the element because no padding or margin has been applied. ](https://hychalknotes.s3.amazonaws.com/box-model-3.png)

Go ahead and add some margin to box1, padding to box2 and both to box3:

```css
.box1 {
  background-color: gold;
  margin: 50px
}
.box2 {
  background-color: paleturquoise;
  padding: 30px;
}
.box3 {
  background-color: lightsalmon;
  padding: 30px;
  margin: 50px;
}
```

![A screenshot of three HTML elements with text inside. There is space between the elements and some space inside of the elements walls and the text illustrating the use of padding and margin.](https://hychalknotes.s3.amazonaws.com/box-model-4.png)

You can see that the background color represents the boundaries of the element.

1. Box 1 has 50px of margin outside of the element, but the text is still squished inside.
2. Box 2 has 30px of padding inside the element, but it's right up against the side of the browser.
3. Box 3 has both, allowing for enough space between both the text and the element above it.

### Specifying sides

We can add padding and margin to a specific side by appending `-[side]` to the property:

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

### Shorthand

When we provide only one value to the `padding` and `margin`, we are telling CSS to give the element padding and margin all around on 4 sides. 

Providing two values means the first value will be used for `top` and `bottom`, second value will be used for `left` and `right`.

Providing three values means the first value will be used for `top`, second value will be used for `left` and `right` and third value will be used for `bottom`. 

Providing four values will specify values for each of the 4 sides. 

```css
/* Apply to all four sides */
padding: 10px;

/* vertical | horizontal */
padding: 10px 20px;

/* top | horizontal | bottom */
padding: 10px 20px 5px;

/* top | right | bottom | left */
padding: 10px 20px 30px 25px;
```

Note: These examples are the valid for `margin` as well. 

### Placing elements with margins

There are times when we want to center an element horizontally and we can use auto margins to achieve that:

```css
.box1 {
  width: 60%;
  margin: 0 auto;
}
```

This will set the top and bottom margins to zero (you could set it to anything you want) and then the left and right margin to `auto`, which centers the element within the browser. Keep in mind that this will only take effect if `width` property is specified. 

<img src="https://hychalknotes.s3.amazonaws.com/margin-auto-1.png" alt="screenshot showing usage of margin auto that centers the element horizontally.">

We can also specify `margin-right: auto` to place the element right-aligned. 

```css
.box1 {
  width: 60%;
  margin-right: auto;
}
```

<img src="https://hychalknotes.s3.amazonaws.com/margin-auto-2.png" alt="screenshot showing usage of margin auto that centers the element horizontally.">


## The `box-sizing` property

Open up [this CodePen](https://codepen.io/susan8098/pen/vYOPeRP?editors=1100).

We see a blue box wrapped inside a light gray container. They are both set to width of 600px.

<img src="https://hychalknotes.s3.amazonaws.com/box-sizing-1.png" alt="a blue container wrapped inside a light gray container with the same width of 600px.">

What if we add some padding and border to the blue box?

```css
.box {
  width: 600px;
  height: 300px;
  background-color: skyblue;

  /* Adding padding and border */
  padding: 20px;
  border: 5px solid tomato;
}
```

<img src="https://hychalknotes.s3.amazonaws.com/box-sizing-2.png" alt="a blue container that appears to be wider sitting on top of the gray container that is 600px wide.">

What happened here? If we use the dev tool to inspect the blue box, we will find out that the blue box is no longer 600px, it is now 650px!

This is because by default, CSS box model calculates the total width and height of the element by taking `padding` and `border` values into account like so:

```bash
width-of-box = width + padding-left + padding-right + border-left + border-right
```
```bash
height-of-box = height + padding-top + padding-bottom + border-top + border-bottom
```

What we initially defined as 600px width now becomes:
```bash
600px(content width) 
+ 20px(padding-left) 
+ 20px(padding-right) 
+ 5px(border-left) 
+ 5px(border-right) = 650px
```

We can use **`box-sizing`** property to override this default, by changing the default value from `content-box` to `border-box`. This will let the browser know **not** to render `padding` and `border` values into the computed size of our element. 

This is a CSS gotcha we almost always want to avoid, which is why it is a good idea to always include this code at the top of our stylesheet. 

```css
* {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
```

The `*` character is a wildcard selector and selects everything on the page. Grab the code from above and add it into the CodePen to see this working.

<img src="https://hychalknotes.s3.amazonaws.com/box-sizing-3.png" alt="a blue box with red border fitted inside a gray container.">

## Exercise

It's time to get comfortable with margin, padding, widths and borders, as well as to brush up on selectors.

Download [css-dimensions-exercise.zip](https://hychalknotes.s3.amazonaws.com/css-dimensions-exercise.zip) and open `css-dimensions-exercise.html` in your editor and browser. You will find a set of instructions in the document.
Open `css-dimensions-exercise-ANSWER.html` from that folder in your browser to see what you are working towards.