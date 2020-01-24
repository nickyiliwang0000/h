<!-- Student takeaway: -->
<!--Student will be able to:
- Name four ways of sizing in CSS (pixel, percentage, em, rem)
- Identify the utility of sizing text in percentage, em, or rem
- Explain how em and rem are different
- Identify two keyword values for sizing (auto, inherit)
 -->

# CSS measurement units

## Measurement units
A lot of CSS is declaring what the size of something will be (e.g. the explicit width of an element or its padding and margin). The web has measurement units specific to screens and browsers - no inches or centimetres here! 

## Pixels
Screens are measured in _pixels_, tiny units specific to digital images. Lots of web content, like images and fonts, are already sized in pixels, which makes them easy to work with on the web. 

```css
h3 {
  font-size: 20px;
}

section {
  max-width: 1080px;
}
```

Most browsers default to a font size of 16px. Larger base font sizes (between 18px and 22px) are becoming more common because they are easier to read. Check out [the web typography lesson](https://github.com/HackerYou/bootcamp-notes/blob/master/css/web-typography.md#sizing-fonts) for more information on sizing fonts.

## Percentages

Another popular way to size fonts and elements is _percentages_, which are indispensible in responsive design. An element whose width is a percentage will take up that percentage of its parent's width. 

```html
<div class="wrapper">
  <main></main>
  <aside></aside>
</div>
```

```css
.wrapper{
  max-width: 1000px;
}

aside {
  width: 25%;
  /* this will be 250px */
}

main {
  width: 75%;
  /* this will be 750px */
}
```

Percentages can also be used for fonts. If the parent has a font size of 20px, a 50% font size would be 10px. 

```css
div {
  font-size: 20px;
}

div p {
  font-size: 50%;
  /* 20px x 0.5 = 10px */
}
```

## Ems

`em` units are similar to percentages in that they take their size from a parent's explicitly declared size. They are commonly used for fonts in this way:

```css
html {
  font-size: 10px;
}

body {
  font-size: 1.6em; /*  10px x 1.6 = 16px */
}
```

An important fact to know about `em` units is that their value _compounds_, meaning it multiplies the value of the font-size in the context where it is applied (ie. its parent's value). This means that the same `font-size` declaration will render different-sized fonts depending on where the element is nested.

```css
html {
  font-size: 10px;
}

body {
  font-size: 1.6em; /*  10px x 1.6 = 16px */
}

body main {
  font-size: 1.6em; /*  16px x 1.6 = 25.6px */
}
```

An alternative to this are `rem` units, which were specifically invented to fix this compounding problem.

## Rems

_Root em units_ (`rem`) are similar to `em` units, as they are calculated by multiplication of another value. However, unlike `em` units, they only refer to the root element (usually the `html` element). Any sizing that uses `rem` will treat the `font-size` of the root element as the basis from which to multiply. 

```css
html {
  font-size: 20px;
}

body {
  font-size: 1rem; /*  20px x 1 = 20px */
}

body main {
  font-size: 1.1rem; /*  20px x 1.1 = 22px */
}
```

Received a design set in pixels? [Check out this resource to help you calculate the `rem` equivalent](https://offroadcode.com/rem-calculator/).

[More info on rems](http://snook.ca/archives/html_and_css/font-size-with-rem)

### Base fonts (setting up for `rem` and `em` units)
When using `rem` and/or `em` units for your site, you will need to set a base font as shown above. Setting your base font to a percentage rather than a fixed pixel value will make your site more accessible to all users.

By default, most browsers will have a default font size of `16px`. However, a user should be able to make this bigger or smaller. When we set the `html` element with a fixed pixel font size (e.g. `20px`), we are overriding our users' browser settings. This is not good for accessibility or user experience. Instead of a fixed pixel value, we can do something like this:

```css
html {
  font-size: 125%; /* 16px * 1.25 = 20px */
}

p {
  font-size: 1.1rem; /* 1.1 * (1.25 * 16) = 22px */
}
```
Setting the base font to a percentage value will help with implementing `rem` units throughout your site, but will also accommodate any custom browser settings.

To calculate the percentage equivalent of your chosen pixel base font. You will want to take your chosen pixel base font and divide it by `16`. `16px`  is the default font size for most browsers, which is why we use it to calculate the percentage equivalent for our base font.


## Advantages to using `%`, `em` and `rem` over `px`

The idea behind sizing fonts in percentage, `em`, or `rem` is that when you want larger font all over the website (e.g. at a small screen size), you only have to bump up the base font size and the rest of the fonts will scale accordingly. 

## Measurement keywords

Sometimes we will be able to supply keywords for sizes of elements and fonts. You will see the keywords `auto` and `inherit` most often.
* `auto` allows an element to automatically size itself based on its surroundings and content.
* `inherit` allows an element to inherit the style from its parent. We will talk about this more in future exercises.

