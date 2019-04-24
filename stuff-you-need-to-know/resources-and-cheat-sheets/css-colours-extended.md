# CSS colors extended

## HSL color
_HSL_, which stands for hue-saturation-light, is a third way defining color. To declare an HSL color, a developer specifies a hue ([number between 0 and 239](https://stackoverflow.com/questions/1290190/why-are-max-values-for-saturation-and-hue-are-240-and-239-respectively)) and percentages (between 0% and 100%) for saturation and light.

| color name | hex value | rgb value| hsl value|
| ---: | --- | --- |---|
| black | `#000000` | `rgb(0, 0, 0)`| `hsl(0, 0%, 0%)`|
| white| `#ffffff` | `rgb(255, 255, 255)`| `hsl(0, 0%, 100%)`|
| red| `#ff0000` | `rgb(255, 0, 0)`| `hsl(0, 100%, 50%)`|
| blue| `#0000ff` |`rgb(0, 255, 0)` | `hsl(240, 100%, 50%)`|


## Alpha channel
The alpha channel is an optional fourth value you can provide to HSL color declarations to acheive a transparent look. When you use the alpha channel, you need to tell the browser you're doing so by using the letter `a` after the `hsl` declaration. Alpha channel values can be percentages or decimals between 0 (totally see-through) and 1 (totally opaque).

`hsla(124,40%,40%,50%)`

## More information about color

### CMYK vs. RGB vs. HSL
There are two sets of color keywords in the CSS3 spec that refer to the same color. `Cyan` and `aqua` are the same and `magenta` and `fuchsia` are the same.

Why? Well. **Get ready.**

Printed or dyed color is different from digital color. We perceive printed or dyed color when light reflects off physical matter. Digital color is made from light. This is why different kinds of screens render color a little differently.

![additive color model diagram](http://www.mobiliodevelopment.com/wp-content/uploads/2012/04/RGB-colors.gif)
* RGB color model
  * Screens (historically computer screens) use the red-green-blue color model. 
  * RGB is additive, which means that the starting point is black (the absence of light) and the opposite end of the spectrum is white light (i.e. the combination of red, green, and blue lights)

![HSL colour wheel](https://uwdigipub.files.wordpress.com/2014/11/hsl-color-wheel-pagespeed-ce-if6-exzipy.png)

* HSL color model
  * Screens (historically TV screens) use the hue-saturation-light model.
  * HSL is additive, like RGB. The `hue` value is a representation of the location around the color wheel. The `saturation` value is how much color is applied (0% = grayscale). The `lightness` value is how illuminated the color is where 0 is black, 100% is white, and the average lightness value is 50%.
  * The [appeal of HSL is](https://www.w3.org/wiki/CSS3/Color/HSL) that changing the numbers changes the color [in a way you would expect](https://css-tricks.com/examples/HSLaExplorer/). 

HSL was created in part as a color model that explicitly takes into account the way colors are organized and conceptualized in human vision. 

![subtractive color model diagram](http://archive.xaraxone.com/webxealot/workbook40/color_01.gif)

* CMYK color model
  * Print uses the cyan-magenta-yellow-black model (the K is for blac**k**).
  * CMYK is subtractive, which means that the starting point is black (all the colors together) and the opposite end of the spectrum is white (i.e. color of the paper).

Most (but not all) colors from RGB can be represented using CMYK. This makes sense; you can make more and finer-grained distinctions with light than with ink.

In each of those models, you can get that <span style="background-color:cyan;">bright blue color</span>.  In RGB, it's in the middle of green and blue and white light and it's called `aqua`. In CMYK, it's a cardinal color called `cyan`. (In HSL, it's at 180°.) We look at color on screens, but our names for the colors come from real life. Having both as CSS color keywords comes from developers having different frames of reference for the colors they're creating on the web. 

For more on colors as they pertain to web development, [check out the W3C's wiki](https://www.w3.org/wiki/CSS3/Color).