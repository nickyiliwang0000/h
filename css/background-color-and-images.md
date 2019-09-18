# Intro to CSS backgrounds

All HTML elements can have backgrounds. The background will appear within the dimensions of the element and behind any content or other elements that are nested within.

The background of an element can be an image, a gradient, one of the color formats we discussed before, or a combination of those.

## Background colour

To provide a background color, use the `background-color` property and pass a color value in.

```css
header {
  background-color: black;
}

section {
  background-color: rgba(0, 255, 0, 0.7);
}

p {
  background-color: #008B8B;
}

h3 {
  background-color: hsla(90, 30%, 94%, 1);
}
```

Use caution when deciding background and text colours combinations. Low contrast can make content difficult or impossible to read. 
> The WCAG AA requires a contrast ratio of 4.5:1 for normal text and 3:1 for large text. Logos or brand names have no contrast requirements or minimums. [This is a great resource](https://www.w3.org/TR/WCAG20#visual-audio-contrast-contrast) for checking colour contrast, and [so is this](http://leaverou.github.io/contrast-ratio/#%23555-on-white).</a>
</div>

## Background images

The CSS property to use an image instead of a colour is  `background-image`. Specifying the value is a little different because we have to tell the CSS where the image we want to use is located. For this we use the value `url()` and pass in the image path.

Just like the `<img>` tag, we can use absolute or relative tags.

```css
body {
  background-image: url(images/dog2.jpg);
}
```

```css
body {
  background-image: url(https://www.google.com/images/srpr/logo3w.png);
}
```

By default, the background image will repeat and appear with its native dimensions.


### When should I use a background image vs. an HTML img element?
When the image matters to the content of your page, use an `img` tag. If the image is purely aesthetic, use a background image. Basically, think about whether you would want a screen reader to describe your content or ignore it. (Background images don't have alt text.)

## Background image properties

When using the background image property, the image will repeat by default from the left to the right, and the top to the bottom. Using the `background-repeat` property, we can specify how the background repeats:

value passed to `background-repeat` | what it looks like
---|---
`no-repeat`| no repeat, show the image only once
`repeat-x` | repeat across the x axis at the image's natural size
`repeat-y` | repeat down the y axis at the image's natural size

### Background positioning

When repeating a background image we need to specify where it repeats from. For this, we use `background-position`. We pass it **two**  pixel, percentage or keyword values which specify the x and y distances of the image from the top-left of the element. The first value will refer to the horizontal position of the background, and the second value will define the vertical position. The left top corner is `0% 0%` or ` 0px 0px`. The right bottom corner is `100% 100%`.

(If you only specify one value, the other will be 50% or `center`.) The `background-position` property accepts the keyword values `top`, `left`, `right`, `bottom` and `center`. The default is `left top`. 

```css
section {
  background-position: left bottom;
}
```

```css
section {
  background-position: center;
}
```

```css
section {
  background-position: 50% 10px;
}
```
Here is [a little demo](https://www.w3schools.com/cssref/playit.asp?filename=playcss_background-position&preval=10px%20200px) where you can play around with background position.
<!-- Background attatchemt -->

### Background attachment

Sometimes you will want to have control over whether a background image is fixed within the viewport or scrolls. For this we use the `background-attachment` property. There are three primary types of attachment: `fixed`, ` scroll`, and `local`. 

`background-attachment: scroll` is the defualt attachment property and will make the background you are targeting scroll relative to the main view but stay fixed in the local view. **Note**: when the background is fixed in the local view, it is attached to the border of that element (more on this below). What this means is it will behave like you would expect, if you scroll the site, the image scrolls along with everything else.

```css
section {
  background-attachment: scroll;
}
```

`background-attachment: fixed` will "fix" the image to the viewport. So even as other content scrolls, the image will stay in its place. This is sometimes used to achieve the a "parallax" scroll effect by fixing an image as a background to other content that will scroll.

```css
section {
  background-attachment: fixed;
}
```

`background-attachment: local` solves a unique problem for us. If the content you are trying to scroll relative to (the local view) has its own scroll bar, `background-attachment: scroll` ends up behaving like `background-attachment: fixed`. The expected behaviour will still apply when you scroll the page (main view) itself. This is because `background-attachment: scroll` stays fixed within its local view.  `background-attachment: local` to the rescue! This fixes the background to the content rather than the border of the element allowing things to scroll along with the page, even when the element it is attached to has its own scroll bar.

```css
section {
 background-attachment: local;
}
```
Here is [a little demo](https://codepen.io/kevinpowell/pen/bzMvzN) to see a comparison of these 3 attachment properties in action!


### Background size properties

The `background-size` property specifies the size of the background image. It allows the image to be scaled up, or constrained within the dimensions of the element.

```css
header {
  background-size: 100px;
}
```
You may be explicit in your sizing if you want the image to repeat but most often you'll be using one of two keywords:

#### `background-size: cover;`

To have the background image take up the entire width of the element use the property of `cover`. If the image ratio is larger than the element itself, it will be cropped.

```css
header {
  background-size: cover;
}
```

#### `background-size: contain;`

This keyword scales the image as large as possible while maintaining its aspect ratio (so the image doesn't get squished).

```css
header {
  background-size: contain;
}
```
## Background shorthand

Writing background properties can take up a lot of space. To save a few lines of CSS, we can use the `background` property, which combines all the background properties except `background-size`. The `background` shorthand includes an optional background color.

```css
body {
  background: [background-color] [background-image] [background-position] [background-repeat] [background-attachment];
}
```

```css
body {
  background: red url(images/dog2.jpg) top right repeat-y fixed;
}
```
## Background gradients

A really cool feature of the background property is the ability to create gradients in pure CSS. Previously, you'd have to export an image of a gradient from something like Photoshop. Now, background gradients can be defined using the `background-image` property, or through the `background` shorthand.

### Linear gradients

To create a linear gradient, we use the `linear-gradient()` property and pass a series of values.

```css
div {
  background: linear-gradient( 45deg, blue, red );
}
```

The values provided are the angle along which the gradient will progress and the colours of the gradient.

```css
div {
  background: linear-gradient( [angle], [colour], [colour] );
}
```

The angle can be provided as a keyword or a value in degrees. By default, gradients originates from the top center of the item.  When using a keyword to define angle, you must also use the word `to`.

```css
ul {
  background: linear-gradient( to bottom, blue, #ffffff );
}

h1 {
  background: linear-gradient( to top right, blue, red );
}
```

The gradient can take as many colours as you'd like. These colours will be spread evenly throughout the gradient by default. Any color definition can be used.

```css
div {
  background: linear-gradient( to right, 
    blue, 
    green,
    hsla(123,23%,15%,0.5), 
    rgb(122,22,55), 
    rgba(12,44,156,0.6), 
    hsl(300,12%, 88%), 
    #bada55)
}
```

To control the position of each colour stop, provide a percentage value next to the colour.

```css
div {
  background: linear-gradient( to right, blue 20%, red 40%, green, yellow, pink, lime 70%);
}
```

### Radial gradients

A radial gradient allows you to create a circular gradient as a background. Its syntax is similar to that of a linear gradient but doesn't require an angle.

```css
aside {
  background: radial-gradient(red, #ffaa88);
}

header {
  background: radial-gradient(red 10%, yellow 25%, lime 75%);
}
```

## Multiple backgrounds

To layer backgrounds on top of one another, comma separate the background values you want:

```css
div {
  background: url(http://www.placekitten.com/200/200), 
    linear-gradient(yellow 20%, red , blue);
    background-repeat: space;
}
```

The `space` value[ isn't supported in all browsers](https://caniuse.com/#feat=background-repeat-round-space) but is included here so you can see what layered background images look like.

Check this code out in [this CodePen](https://codepen.io/zkdan/pen/ZmKGMW).

Note that the first background defined here is the one on top. Try changing the order of the backgrounds and see what happens.
