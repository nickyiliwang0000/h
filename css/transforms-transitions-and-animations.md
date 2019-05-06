# Transforms, transitions, and animations

## CSS transitions

So far we have worked with hover states where an item goes from A to B in a split second - a hard transition. If we have an element that's naturally 200px wide and grows to 500px wide on hover, it just snaps to that size.

CSS allows us to animate the transition between A and B (or normal and hover state).

Create a new HTML file, and add the following markup and styles:

```html
<div class="galleryItem"></div>
```

and

```css
.galleryItem {
  width: 200px;
  height: 200px;
  background: red;
}

.galleryItem:hover {
  width: 500px;
}
```

What if we wanted to animate it from 200px to 500px instead of the harsh snap to 500px? Well, that's where we are able to use _CSS3 transitions_.

By simply appending a CSS property called `transition` and then specifying which property should be animated and for how long we can add animation.

```css
.galleryItem {
  width: 200px;
  height: 200px;
  background: red;
  transition: width 1s;
}

.galleryItem:hover {
  width: 500px;
}
```

Notice how we only added `transition: width 1s;` to the CSS? You'll often see the time written as `1s`, representing one second.

You can animate almost any property: `width`, `height`, `padding`, `margin`, `border` and even `background-color`, just simply provide the property name!
<a href="https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_animated_properties" target="_blank">See a list of animatable properties here</a>.

```css
.galleryItem {
  width: 200px;
  height: 200px;
  background: red;
  transition: background 1s;
}

.galleryItem:hover {
  width: 500px;
  background: yellow;
}
```

### `transition-timing-function`

The third optional value that transition can take is the `transition-timing-function`. This property will tell the element how to accelerate through the transition. This can help our transitions look more natural, because rarely in life do things move at the same rate throughout a movement.

This property has some keyword values we can use:

- `ease` the element will change slowly both at the beginning and end, and speed up in the middle. This is the _default_ value
- `ease-out` the transition will move quickly at the beginning, and then slow down as it finishes
- `ease-in` the transition will move slow at the beginning and then speed up as it finishes
- `ease-in-out` the transition will move slow at the beginning, speed up in the middle, and slow down as it finishes. It is similar to the ease function.
- `linear` the transition will move at the same rate throughout

We can also create **custom easing** as well, with a _cubic Bézier_. A `cubic-bezier` is a function that represents the progression of the transition over time.
Open up <a href="http://cubic-bezier.com/" target="_blank">http://cubic-bezier.com/</a> to see this in action. You can move the blue and pink dots to change the curve of the graph, which will change the easing of the transition. In order to use this custom easing, all we need to do is copy the cubic-bezier function - which should look something like this: `cubic-bezier(.12,.67,.88,.29)` - and paste it into your `transition` property or `transition-timing-function` property.

🔥 **Hot Tip: there is a cubic bezier creator in the dev tools** 🔥
![Image of the cubic bezier creator in the dev tools](https://hychalknotes.s3.amazonaws.com/Screen%20Shot%202017-08-15%20at%2012.22.29%20PM.png)

```css
transition: all 1s cubic-bezier(0.12, 0.67, 0.88, 0.29);
```

OR

```css
transition-timing-function: cubic-bezier(0.12, 0.67, 0.88, 0.29);
```

![easing example](https://hychalknotes.s3.amazonaws.com/transitionEasing.gif)

### Multiple values

To transition multiple properties, simply comma separate the values. In this example, I've set different times for each of them.

```css
.galleryItem {
  width: 200px;
  height: 200px;
  background: purple;
  transition: background 1s, height 10s, width 0.5s;
}

.galleryItem:hover {
  width: 500px;
  height: 500px;
  background: yellow;
}
```

### The `all` keyword!

You can also use the `all` keyword to transition multple properties. Be cautious with this keyword because it can slow down mobile phones and cause flickering, but it's fun to play with on the desktop. Morph everything!

```css
.galleryItem {
  width: 200px;
  height: 200px;
  background: purple;
  color: white;
  transition: all 2s;
  box-sizing: border-box;
}

.galleryItem:hover {
  width: 500px;
  height: 500px;
  border: 10px dotted green;
  background: yellow;
  border-radius: 50%;
  padding: 10%;
  margin: 50px;
  text-align: center;
  box-shadow: 0 0 20px red;
  color: black;
}
```

What happens if you put one transition on the initial state of an element, but then a different transition on the hover state?

## CSS transforms

_CSS transforms_ allow us to transform an element in two and three dimensions.

The CSS property for transforms is `transform`, and the values you provide define how the element is transformed.

Create an HTML file and add the following code:

```html
<div class="galleryItem"></div>
```

```css
.galleryItem {
  width: 200px;
  height: 200px;
  background: orangered;
}
```

### `transform: rotate()`

By providing a value of rotate, along with a number representing the degrees to rotate, we can rotate an element:
```css
.galleryItem {
  width: 200px;
  height: 200px;
  background: orangered;
  transform: rotate(60deg);
}
```

You can also apply these effects on hover:
```css
.galleryItem {
  width: 200px;
  height: 200px;
  background: orangered;
  transform: rotate(60deg);
}

.galleryItem:hover {
  transform: rotate(180deg);
}
```

Using CSS transitions, we can animate between the two transformed states:
```css
.galleryItem {
  width: 200px;
  height: 200px;
  background: orangered;
  transform: rotate(60deg);
  transition: transform 0.8s;
}

.galleryItem:hover {
  transform: rotate(180deg);
}
```

> When transitioning between different transform values, you can't provide `transition: rotate 1s`. You provide only the property name to transition (e.g. `transform`). You can also use the keyword `all`.

To work within a 3D space, we can use properties that affect the rotation across different planes.

#### `rotateY`

To rotate across the Y axis, use the value `rotateY()`.

```css
.mySquare {
  width: 200px;
  height: 200px;
  background: orangered;
  transform: rotateY(60deg);
  transition: all 0.8s;
}

.mySquare:hover {
  transform: rotateY(180deg);
}
```

### `scale()`

The `scale()` value scales an element to be larger or smaller. Let's take the same 200px by 200px block.

The value of scale is a multiple of the original element. So `scale(1)` would be the original element. `scale(2)` would be twice the size. The footprint that the item takes up remains, yet the item will appear to be larger.

```css
.galleryItem {
  width: 200px;
  height: 200px;
  background: orangered;
  transition: all 0.8s;
}

.galleryItem:hover {
  transform: scale(2.2);
}
```

As with the last one, we can also animate them.  

Note: You may see some screen flickering on mobile devices or even desktop browsers.

```css
.image {
  transition: all 0.5s;
}

.image:hover {
  transform: scale(2);
}
```

```html
<img src="https://unsplash.it/200/200/?random" class="image" />
<img src="https://unsplash.it/200/200/?random" class="image" />
<img src="https://unsplash.it/200/200/?random" class="image" />
<img src="https://unsplash.it/200/200/?random" class="image" />
```

![four images, scale on hover example](https://hychalknotes.s3.amazonaws.com/transform-scale-img-example.png)

### Scaling x and y

While the `scale()` property handles the image as a whole, you can utilize the `scaleX()` and `scaleY()` properties to scale an element across certain axis'.

```css
.image {
  transition: all 0.5s;
}

.image:hover {
  transform: scaleX(2);
}
```

### Multiple transforms

There are many more values available that can be used to create really cool effects. Take a look at the available values [on MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/transform).

### Multiple values

You'll notice that in the above examples, we've provided a single value, however, you'll often want to change multiple properties.

In order to add multiple properties to the transform property use a space to seperate each value.

```css
.galleryItem {
  width: 200px;
  height: 200px;
  background: orangered;
  transform: rotate(60deg) scaleX(2) scaleY(1.4);
  transition: all 0.8s;
}

.galleryItem:hover {
  transform: rotate(180deg) scaleX(2) scaleY(1.4);
}
```

To transition these properties, we have to provide all the values again, including the one we want to change.

### Transform exercise

Transforms can be used for some pretty interesting effects. Download (transform-transition-bootcamp.zip](https://hychalknotes.s3.amazonaws.com/transform-transition-bootcamp.zip) and try to recreate the answer key!

## CSS animations

We have talked about both transitions and transforms so far, now let's take a look at using `keyframes` to produce animations. Again, these tools should be vendor prefixed in older browsers.

_Key frames_ define different points in an animations life-time. We use percentages to mark different points within the keyframe. Here is a very simple example:

First, we need to create the animation. Unlike most css, we do this outside of the element we want to apply it to, in its own CSS rule:

```css
@keyframes snow {
  0% {
    top: 0;
  }

  100% {
    top: 100%;
  }
}
```

You are able to specify any percentage along the way, `0%` and `100%` representing the start and finish of the animation. If you have multiple points where you want to apply the same values, you can comma separate the percentage points:

```css
@keyframes snow {
  0% {
    top: 0;
  }

  20%,
  40%,
  60%,
  80% {
    margin-left: 100px;
  }

  10%,
  30%,
  50%,
  70%,
  90% {
    margin-left: 10px;
  }

  100% {
    top: 100%;
  }
}
```

Now, that doesn't do anything except make an animation called `snow`. We need to apply it to our element.

```html
<div class="snowflake snowflake1">&#10052;</div>
<!-- unicode snowflake -->
```

```css
@keyframes snow {
  0% {
    top: 0;
  }

  100% {
    top: 100%;
  }
}

/* Apply our snow animation */
.snowflake {
  position: absolute;
  font-size: 40px;
  color: white;
  animation: snow 3s linear infinite;
}
```

`animation: snow 3s linear infinite;` took four arguments.

* `snow` is the animation name. This is the same as what we name our keyframes
* `3s` is the duration it takes to complete the animation
* `linear` is something we call _easing_. Easing allows you to make smoother animations - not what we want in this case. You can choose from `ease-in`, `ease-out`, `ease-in-out` or `linear`. This can also be a `cubic-bezier`. [Check out this great visual resource to create your own cubic-beziers](http://cubic-bezier.com/#.17,.67,.83,.67).
* `infinite` defines the iteration. You could also set a number here and specify how many times animation should run.

You can also set them independently as well as add a few other options:

```css
.snowflake {
  animation-name: snow;
  animation-duration: 20s;
  animation-timing-function: linear;
  animation-delay: 1s;
  animation-iteration-count: 2;
  animation-direction: alternate;
  animation-fill-mode: both;
}
```

* `animation-delay` will tell the animation to wait a set amount of time and then run.
* `animation-direction` will tell the animation to play forwards, backwards, or alternate forwards then backwards. Keywords to use with this property are:
  * `normal` (for forwards)
  * `reverse` (for backwards)
  * `alternate` (to alternate back and forth)
  * `alternate-reverse` (to alternate, but start backwards then go forwards)
* `animation-fill-mode` will tell the element what styles should be applied when the animation is not active. An animation is considered not active, when it has ended or if there is a delay. Keywords to use with this property are:
  * `none` It's the default and the element will not take any styles defined in the keyframe.
  * `forwards` When the animation ends, the element will hold onto the styles applied during the last part of the animation (`animation-direction` can affect which set of styles are considered as the "last part of the animation").
  * `backwards` During a delay (defined by `animation-delay`), the element will take on the styles that will be applied during the first part of the animation (`animation-direction` can affect which set of styles is considered as the “first part of the animation").
  * `both` During an `animation-delay`, it will take on the styles that will be applied during the first part of the animation. Once the animation ends, it will also hold on to the styles applied during the last part of the animation.

Check out this [video](https://www.youtube.com/watch?v=irJXZnA3g5U) to see `animation-fill-mode` in action.

## Animation libraries

One of the great parts of this community is that people are creating tools that we can freely use in our projects. Since animations can often be time-consuming, a couple libraries of keyframe animations exist and that you can use them in your projects.

* [Magic Animations](http://www.minimamente.com/example/magic_animations/)
* [CSS3 Animation Cheat Sheet](http://www.justinaguilar.com/animations/index.html#how)
* [Animista](http://animista.net/)
* [Animate.css](http://daneden.github.io/animate.css/)

## More animation exercises

Looking for more exercises to do on your own? Download the files below for more practice!

* [Starter files and answer key](https://hychalknotes.s3.amazonaws.com/shooting-star-animation.zip) for a shooting star animation.
* [Starter files and answer key](https://hychalknotes.s3.amazonaws.com/shape-animation.zip) for a shape morphing animation.
* [Starter files and answer key](https://hychalknotes.s3.amazonaws.com/using-animate.css-library.zip) for using Animate.css, and optionally creating your own animations.
* [Starter files and answer key](https://hychalknotes.s3.amazonaws.com/wombly-path-svg-exercise.zip) to animate an SVG.
* Open up [these files](https://hychalknotes.s3.amazonaws.com/jquery-and-animate-bootcamp.zip) and use Animate.css to animate the text on click.
<!-- Open up <a href="https://hychalknotes.s3.amazonaws.com/animate.html" class="exercise" download>animate.html</a> and let's load in animate.css. -->
