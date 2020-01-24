<!-- Student takeaway: -->
<!--Student will be able to:
- Name the three standard color formats
- Identify which of the three standard color formats accept alpha values
- Use a alpha channel color to make a heading's background partially see-through
 -->
# Intro to CSS colours

Colour is an important part of styling. Choosing the right format for colour can help acheive the look you (or your designer) wants.

> In CSS, the color property is spelled `color`, not `colour` because CSS was created in the US. **¯\\\_(ツ)_/¯**

There are six different formats that can be used as a ~~colour~~ color value for a property.
* CSS color keyword
* Hexadecimal
* RGB
* RGBA
* HSL
* HSLA

Our focus will be directed more towards the first four formats. You can learn more about HSL and HSLA [here](https://github.com/HackerYou/bootcamp-notes/blob/master/stuff-you-need-to-know/resources-and-cheat-sheets/css-colours-extended.md).

## CSS color keywords 

There are 140 standard css colors, with 16 of them represented by basic color keywords. Any color keyword can be given as a value to a property that accepts colour.

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

You can also find a nice grouping of similar colors at w3school's website [here](https://www.w3schools.com/colors/colors_groups.asp).

## Hexadecimial color

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
| blue| `#0000ff` |`rgb(0,0,255) `|


## Alpha channel
The alpha channel is an optional fourth value you can provide to HSL and RGB color declarations to achieve a transparent look. When you use the alpha channel, you need to tell the browser you're doing so by using the letter `a` after the `rgb` declaration. Alpha channel values can be percentages or decimals between 0 (totally see-through) and 1 (totally opaque).


`rgba(0,255,100,.5)`

Mess with the values [in this CodePen](https://codepen.io/hackeryou/pen/YRyQvR) to see how the alpha channel works.

<!-- <iframe src="https://codepen.io/hackeryou/pen/YRyQvR" height="400" width="600"></iframe> -->

### Opacity vs. alpha channel
Take a look at [this CodePen](https://codepen.io/hackeryou/pen/QJjgNL) and figure out the difference between the CSS property `opacity` and the alpha channel.
<!-- Explain to students that opacity affects all of an element's children -->
<!-- <iframe src="https://codepen.io/hackeryou/pen/QJjgNL" height="400" width="600"></iframe> -->





