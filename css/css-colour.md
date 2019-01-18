<!-- Student takeaway: -->
<!--Student will be able to:
- Name the three standard color formats
- Identify which of the three standard color formats accept alpha values
- Use a alpha channel color to make a heading's background partially see-through
 -->
# Intro to CSS Colours

Colour is an important part of styling. Choosing the right format for colour can help acheive the look you (or your designer) wants.

> In CSS, the color property is spelled `color`, not `colour` because CSS was created in the US. **¯\\\_(ツ)_/¯**

There are six different formats that can be used as a ~~colour~~ color value for a property.
* CSS color keyword
* Hexadecimal
* RGB
* RGBA
* HSL
* HSLA

## CSS color keywords 
There are 16 basic color keywords in CSS and 131 extended color keywords. Any color keyword can be given as a value to a property that accepts colour.

The 16 basic keywords:
* black
* silver
* gray
* white
* maroon
* red
* purple
* fuchsia
* green
* lime
* olive
* yellow
* navy
* blue
* teal
* aqua

A selected list of the extended ones:
* crimson
* peachpuff
* dodgerblue
* orchid
* rebeccapurple

To view the full list of color names available, visit [this cute website](http://colours.neilorangepeel.com/) or see the W3C spec [here](https://www.w3.org/TR/css-color-3/#notes).

## Hexadecmial color

A common way to provide color is to use the _hexadecimal system_. The codes or values produced by this system are sets of alphanumeric characters prepended by a `#`.

Some common colors are:

| color name | hex value |
| ---: | --- |
| black | `#000000` |
| white| `#ffffff` |
| red| `#ff0000` |
| blue| `#0000ff` |

Hex codes are made up of three pairs of alphanumeric digits that represent red, green, and blue respectively. The characters that can be used range from 0-9 and a-f (or A-F hex codes are not case-sensitive). 

![diagram explaining each set of numbers in a hex code](https://hychalknotes.s3.amazonaws.com/hex-codes-case-insensitive.png)

It's hard to create a hex code from scratch because the matrix used to calculate the colors is not intuitive. Don't worry about it too much right now.

### Shorthand

Hex values can be shortened into three digits if the two digits that represent each color value are the same.
![screenshot of shortened hex code in Visual Studio Code showing that it's the same as a longer hex code](https://hychalknotes.s3.amazonaws.com/hex-codes-shortened.png)

## RGB color
_RGB_ is another way of defining color. RGB stands for red-green-blue; to declare an RGB color, a developer specifies a value between 0 (black) and 255 (white) for each component color.

Some common colors are:

| color name | hex value | rgb value|
| ---: | --- | --- |
| black | `#000000` | `rgb(0,0,0)`|
| white| `#ffffff` | `rgb(255,255,255)`|
| red| `#ff0000` | `rgb(255,0,0)`|
| blue| `#0000ff` |`rgb(0,255,0) `|

## HSL color
_HSL_, which stands for hue-saturation-light, is a third way defining color. To declare an HSL color, a developer specifies a hue ([number between 0 and 239](https://stackoverflow.com/questions/1290190/why-are-max-values-for-saturation-and-hue-are-240-and-239-respectively)) and percentages (between 0% and 100%) for saturation and light.

| color name | hex value | rgb value| hsl value|
| ---: | --- | --- |---|
| black | `#000000` | `rgb(0, 0, 0)`| `hsl(0, 0%, 0%)`|
| white| `#ffffff` | `rgb(255, 255, 255)`| `hsl(0, 0%, 100%)`|
| red| `#ff0000` | `rgb(255, 0, 0)`| `hsl(0, 100%, 50%)`|
| blue| `#0000ff` |`rgb(0, 255, 0)` | `hsl(240, 100%, 50%)`|

## Alpha channel
The alpha channel is an optional fourth value you can provide to HSL and RBG color declarations to acheive a transparent look. When you use the alpha channel, you need to tell the browser you're doing so by using the letter `a` after the `rgb` or `hsl` declaration. Alpha channel values can be percentages or decimals between 0 (totally see-through) and 1 (totally opaque).

|rgba|hsla|
---|---
`rgba(0,255,100,.5)` | `hsla(124,40%,40%,50%)`

Mess with the values [in this CodePen](https://codepen.io/hackeryou/pen/YRyQvR) to see how the alpha channel works.

<!-- <iframe src="https://codepen.io/hackeryou/pen/YRyQvR" height="400" width="600"></iframe> -->

### Opacity vs. alpha channel
Take a look at [this CodePen](https://codepen.io/hackeryou/pen/QJjgNL) and figure out the difference between the CSS property `opacity` and the alpha channel.
<!-- Explain to students that opacity affects all of an element's children -->
<!-- <iframe src="https://codepen.io/hackeryou/pen/QJjgNL" height="400" width="600"></iframe> -->

## More information about color

### CMYK vs. RGB vs. HSL
There are two sets of color keywords in the CSS3 spec that refer to the same color. `Cyan` and `aqua` are the same and `magenta` and `fuchsia` are the same.

Why? Well. **Get ready.**

Printed or dyed color is different from digital color. We perceive printed or dyed color when light reflects off physical matter. Digital color is made from light. This is why different kinds of screens render color a little differently.

![additive color model diagram](http://www.mobiliodevelopment.com/wp-content/uploads/2012/04/RGB-colors.gif)
* RBG color model
  * Screens (historically computer screens) use the red-blue-green color model. 
  * RBG is additive, which means that the starting point is black (the absence of light) and the opposite end of the spectrum is white light (i.e. the combination of red, green, and blue lights)

![HSL colour wheel](https://uwdigipub.files.wordpress.com/2014/11/hsl-color-wheel-pagespeed-ce-if6-exzipy.png)

* HSL color model
  * Screens (historically TV screens) use the hue-saturation-light model.
  * HSL is additive, like RBG. The `hue` value is a representation of the location around the color wheel. The `saturation` value is how much color is applied (0% = grayscale). The `lightness` value is how illuminated the color is where 0 is black, 100% is white, and the average lightness value is 50%.
  * The [appeal of HSL is](https://www.w3.org/wiki/CSS3/Color/HSL) that changing the numbers changes the color [in a way you would expect](https://css-tricks.com/examples/HSLaExplorer/). 

HSL was created in part as a color model that explicitly takes into account the way colors are organized and conceptualized in human vision. 

![subtractive color model diagram](http://archive.xaraxone.com/webxealot/workbook40/color_01.gif)

* CMYK color model
  * Print uses the cyan-magenta-yellow-black model (the K is for blac**k**).
  * CMYK is subtractive, which means that the starting point is black (all the colors together) and the opposite end of the spectrum is white (i.e. color of the paper).

Most (but not all) colors from RGB can be represented using CMYK. This makes sense; you can make more and finer-grained distinctions with light than with ink.

In each of those models, you can get that <span style="background-color:cyan;">bright blue color</span>.  In RBG, it's in the middle of green and blue and white light and it's called `aqua`. In CMYK, it's a cardinal color called `cyan`. (In HSL, it's at 180°.) We look at color on screens, but our names for the colors come from real life. Having both as CSS color keywords comes from developers having different frames of reference for the colors they're creating on the web. 

For more on colors as they pertain to web development, [check out the W3C's wiki](https://www.w3.org/wiki/CSS3/Color).


