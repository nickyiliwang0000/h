<!-- Student Takeaway -->
<!-- By the end of this lesson students should be familiar with: colour contrast requirements, browser zoom requirements, flexbox cautions, ways that hiding elements affect screen readers, creating custom focus indicators, what the reduced motion media query is and how to use it. -->

# Accessibility and CSS

We've looked at how HTML choices impact accessibility. But CSS has a lot to be considered as well! Let's explore how the visual layer of our websites and applications impact accessibility.

## Colour Contrast

By far the largest group of accessibility failures are related to colour contrast ratio. It's important for us to check all of the colour contrast ratios for the text we put in front of backgrounds. There are some tools we can leverage to help us with this.

### AA

In order to meet AA compliance we need **regular text** to have a contrast ratio of **4.5:1**. **Large text** (think headings) only needs a contrast ratio of **3:1**. It's important to note that both font size and boldness can impact the required contrast. Thinner text will need more contrast. Sometimes even the font family can have an impact!

### AAA 

If you are looking to be as accessible as possible (which we recommend 😎) why not shoot for AAA contrast compliance? To achieve this the ratio for **regular text** is **7:1** and **large text** is **4.5:1**.

**Some gotchas**! These requirements also apply to images of text, though there is an exception for logo fonts. Also watch out for text over background images, especially moving/animated backgrounds. These can definitely lead to contrast failures.

### Contrast Tools

This tool from [colour safe](http://colorsafe.co/) allows you to choose a background colour, font-family, font-size, font-weight and desired compliance level (A, AA, AAA) and will generate a palette for you! 

With the [Web AIM Colour Contrast Checker](https://webaim.org/resources/contrastchecker/) we can enter both the text and background colours to check their ratio and even play with them using slider tools until we have achieved the required ratio.

The Firefox dev tools also have a cool contrast checker tool. If you inspect an element's colour and click on the colour circle a popup appears that shows the ratio and has sliders allowing you to adjust and test right in the browser!

![Colour Contrast Checker](https://hychalknotes.s3.amazonaws.com/firefox_contrast_checker.png)

## Browser/Text Zoom

A lot of users out there rely on the ability to zoom in on the text in the browser. This can be achieved in different ways for different browsers. This is one of the many reasons why we recommend using `rem`! If the user scales the root size, all of the fonts that have been set relative to the root will scale appropriately. The requirement to achieve AA compliance is that users be able to zoom by **200%** without the document flow breaking (think unpredictable text overlapping etc). To achieve AAA compliance users need to be able to zoom by **400%**.

## Flexbox Cautions

Flexbox is the best, we can achieve many amazing layouts with it! But just one caution in terms of accessibility. If you are re-ordering content with flexbox using properties like flex-direction and order, be sure this layout decision does not reflect any important meaning. The order of the document itself is what will be read by a screen reader. So if you've used flexbox to make an element appear before something else and this is the order in which a screen reader should become aware of this content, then you have failed some users. As a precaution, test by making sure that the order of the content makes sense when CSS is disabled.

## Hiding elements

There are a few ways of hiding elements, but they all have impacts on accessibility. If we use the property `display-none` the element is essentially not in the DOM. This means it will not be read by a screen reader. If we use `visibility: hidden` there will still be a visual footprint, but again, the screen reader will ignore the element. If you want to hide an element but have it read by a screen reader we recommend using some custom CSS often referred to as `sr-only` or `visually-hidden`. The best practice for this could evolve over time, but the currently recommended CSS for this class is:

```css
.visually-hidden:not(:focus):not(:active) { 
  position: absolute !important;
  height: 1px; 
  width: 1px;
  overflow: hidden;
  clip: rect(1px 1px 1px 1px); /* IE6, IE7 */
  clip: rect(1px, 1px, 1px, 1px);
  white-space: nowrap; /* added line */
}
```

## Prefers Reduced Motion 

A lot of users have sensitivity to motion and audio on the web. It is important to give them a way to specify that they would like to stop videos and music and audio, this is referred to as "start, stop, hide" in the WCAG guidelines.

In terms of animations, there is a very handy media query we can use to specify some other CSS as an alternative to an animation, something like a static image. If the user specifies in their browser that they prefer reduced motion this fallback will kick-in.

```CSS
@media (prefers-reduced-motion: reduce) {
 //target things with animations and transitions to turn them off here
}
```