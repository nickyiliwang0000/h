<!-- Student takeaway: -->
<!--Student will be able to:
- Embed and use a Google font
- Know how to find out what font a website is using
-->

# Using web fonts

Waaaaay back in the Middle Ages developers had to use font stacks that were _web safe_, which meant that a good percentage of users was likely to have at least one of them installed on their computers. This was a bummer because it meant that font stacks were like 10 deep and all of them were system fonts. When developers wanted to use cool **new** fonts, they had to save the text as a graphic in Photoshop and export it as an image.

No longer! Now, we can link font files directly in our CSS or use a CDN like [TypeKit](http://typekit.com) (paid) or [Google Web Fonts](http://www.google.com/webfonts) (free).

## Embedding a Google web font

Using Google web fonts is free and pretty easy!

1. Head on over to [Google Web Fonts](ttp://www.google.com/webfonts) and track down a font you like

1. Click the "plus" icon for quick use:

   ![screenshot of google fonts interface for adding a font](https://hychalknotes.s3.amazonaws.com/google-fonts-interface-plus-sign.png)

1. Choose the weights that you wish to use
   ![screenshot of google fonts font weight interface](https://hychalknotes.s3.amazonaws.com/google-fonts-font-weight-interface.png)

   - Note that the more fonts and the more weights you add to a page, the slower your page will load. Try not to include more that 3-4 fonts/weights in production code.

1. Some fonts have extended character sets available if your website will be in a language such as Russian or Vietnamese.

   ![screenshot of google fonts languages interface](https://hychalknotes.s3.amazonaws.com/google-fonts-languages-interface.png)

1. In the next step, click the 'Standard' if it isn't already selected and copy the code provided.

   ![screenshot of google fonts embed interface](https://hychalknotes.s3.amazonaws.com/google-fonts-embed-interface.png)

1. Paste that line of code into the `<head>` of your document

1. You can now use the value of the font name in your `font-family` stack, just as you would any other font. Google will recommend a font stack for you to use:

   ![font stack recommendation](https://hychalknotes.s3.amazonaws.com/google-fonts-font-stack.png)

You may want to apply it to all text on the body:

```css
body {
  font-family: "Open Sans", sans-serif;
}
```

Or just your headers:

```css
h1,
h2,
h3,
h4,
h5,
h6 {
  font-family: "Open Sans", sans-serif;
}
```

### Trying it yourself

Go ahead and pick a few fonts that you like from Google Web Fonts and follow the instructions in [this file](https://hychalknotes.s3.amazonaws.com/web-fonts-exercise-bootcamp.zip).

## Using a paid font

When you use a paid font, you host the font files either from your website or fromt a CDN like TypeKit. We're not going to do an example in class but if you find yourself interested in using font files already on your computer, check out [this resource](https://css-tricks.com/snippets/css/using-font-face/).

## What font is this website using?

<!-- Note that this is extra content; you don't have to get into it in the lesson -->

Have you ever been to a website that just **feels** good? It's probably because of the typography.

You can find out which fonts a website is using by going to the 'Computed' tab in the dev tools and scrolling down to `font-family`.

![screen shot of computed font property on AirBNB](https://hychalknotes.s3.amazonaws.com/computed-font-property.png)

You can also install browser extensions like:

* [What Font?](https://chrome.google.com/webstore/detail/whatfont/jabopobgcpjmedljpbcaablpmlmfcogm) for Chrome
* [Type Sample](http://www.typesample.com/) for Chrome
* [Fontface Ninja](https://addons.mozilla.org/en-US/firefox/addon/fontface-ninja/) for Firefox
* [Font Finder](https://addons.mozilla.org/en-US/firefox/addon/font-inspect/) for Firefox
