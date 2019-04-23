<!-- Student takeaway: -->
<!--Student will be able to:
- Write a font stack
- Correctly predict which font will render in a user's browser
- Use any of the font properties mentioned
 -->

# Web typography

Having beautiful typography is one of the easiest ways to make your site look amazing.

## Declaring fonts

The browser default for typographical elements is typically a serif font like Times New Roman. To change an element's font, we can use the `font-family` property. `font-family` takes the name of a font as a value:

```css
body {
  font-family: "Georgia";
}
```

Or, a font-family:

```css
body {
  font-family: serif;
}
```

The standard font families are:

* serif (e.g. Times New Roman, Georgia)
* sans-serif (e.g. Arial)
* cursive (e.g. Zapf-Chancery)
* fantasy (e.g. Western)
* monospace (e.g. Courier)

If you specify the name of the font (and the user's browser/computer has that font installed), your element will be rendered in the named font. If you specify a `font-family`, the browser/computer will choose the best match from the installed fonts (e.g. `sans-serif` renders Arial on a Windows computer and Helvetica on a Mac).

### Font stacks

Let's say we have a font called `WoweeWhatACoolFont` that I have downloaded from the internet and installed on my comptuer. If I wrote the CSS below:

```css
body {
  font-family: "WoweeWhatACoolFont";
}
```

...and looked at this page in my browser, I'd see a **very cool** font. However, when I put my site up online, anyone who doesn't have `WoweeWhatACoolFont` installed will see the browser default (probably Times New Roman).

To prevent this disappointment, we use a _font stack_. A font stack is a list of fallback fonts for the browser:

```css
body {
  font-family: "WoweeWhatACoolFont", "Zapf-Chancery", cursive;
}
```

The code above checks for `WoweeWhatACoolFont`. If it isn't found, it checks for `Zapf-Chancery`. If that isn't found, the `body` will be rendered in the default cursive font for that computer.

An excellent resource for building fail-proof font stacks is [http://cssfontstack.com/](http://cssfontstack.com/). Let's take a look.

## Sizing fonts

The `font-size` property is pretty self-explanatory. It takes pixels, percentages, `em`, and `rem` values.

Check out `CSS measurement units` for info on how to size fonts with `em`, `rem` and percentages.

The font size you set on the `body` is inherited by all the `<p>` tags on the page. The default font size on most browsers is 16px. Some websites, like the micro-blogging platform [Medium](https://medium.com/@martin.breuss/finding-a-useful-dictionary-api-52084a01503d), have a default font size of 21px. Digital magazine [The Outline](https://theoutline.com/post/6447/ethics-in-news-consumption?zd=1&zi=6alzzi65) defaults to 18px.

Larger font sizes are easier to read. When choosing font sizes for your site, consider your intended audience and the amount of reading you expect them to do.

## Font properties

### `font-weight`

Designers will know that fonts come with a variety of weights. `font-weight` controls how fat or thin the strokes that make up the letters are. Most fonts have at least two weights: `normal` and `bold`, but some can have up to nine different weights. You can specify `font-weight` in CSS with either the keyword or the number:

```css
h3 {
  font-weight: bold; /* Also accepted: bold, bolder, lighter, normal, inherit */
}

h4 {
  font-weight: 600; /* From 100 to 900 in increments of 100 */
}
```

If you specify a weight the font doesn't have, it will fall back to one it does have.

### `font-style`

`font-style` is mostly used to italicize text. `font-style: italic;` will show the explicitly italic character set while `font-style: oblique;` will seem to italicize a font that does not have an italic version.

```css
h5 {
  font-style: italic; /* Also accepted: normal, oblique, and inherit */
}
```

### `line-height`

`line-height` lets you explicitly set the height of a line of text in the browser. Designers may know this as _leading_. This can dramatically help the readability of large blocks of text.

As with most text properties, we can set the value in pixels, `rem`, `em`, or percentages.

```css
h1 {
  font-size: 80px;
  line-height: 91px;
}

p {
  font-size: 10px;
  line-height: 120%; /* Computed line height will be 12px */
}
```

We can also set it as a number, which is used as a multiplier of the font's size.

```css
p {
  font-size: 22px;
  line-height: 2; /* Computed line height will be 44px */
}
```

Most fonts have a default line height of 1.2.

### `text-align`

`text-align` - surprise! - aligns text.

```css
p {
  text-align: right; /* Also accepted: left, center, justify */
}
```

### `text-transform`

`text-transform` is an extremely handy property. We've said a million times that your HTML should only describe the content of your site. What happens when you have a design that relies on either all caps or all lowercase letters?

You can type it however you want and change with `text-transform`.

```css
h1 {
  text-transform: uppercase; /* Also accepted: lowercase, capitalize , inherit */
}
```

It's best practice to only use uppercase for short words and sentences because using all capitals can be difficult to read. Also, screen readers can sometimes misinterpret all capitals as acronyms and read the letters individually. `CONTACT US` becomes `CONTACT U.S.`

### `text-decoration`

`text-decoration` is mostly used to add or remove an underline on links.

```css
a {
  text-decoration: none; /* Also accepted: underline, overline, line-through*/
}
```

### `text-shadow`

This property allows us to apply shadows to our text. With the right colours and techniques, it can [look](https://codepen.io/juanbrujo/pen/yGpAK) [really great](https://codepen.io/hugo/pen/nwivF)! A little text-shadow can also [make your text more legible](https://twitter.com/steveschoger/status/880449411150753792).

`text-shadow` takes four values: horizontal offset, vertical offset, blur, and colour.

```css
h4 {
  text-shadow: 10px 20px 2px black;
}
```

It can also take multiple comma-separated values so you can add as many shadows to your text as you wish! Add some more shadows to [this CodePen](https://codepen.io/zkdan/pen/XygdxX).

### `letter-spacing`

`letter-spacing` (this is gonna blow your mind) allows you to control the amount of space between letters.

Headers look great with a bit less spacing. Uppercase words look great with a little **extra** letter spacing. Mess around with [this CodePen](https://codepen.io/zkdan/pen/WYOwVq)!
