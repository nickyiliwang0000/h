<!-- Student takeaway -->
<!-- By the end of this lesson, the student should know:
- What a favicon is
- The optimal dimensions for favicons and Apple Touch icons
- How to use Font Awesome
-->
# Icons
## Favicons

Favicons are those little images that show up in your browser tab:

![Favicons in the wild](https://hychalknotes.s3.amazonaws.com/favicons-in-the-wild.png)

Choose a favicon by providing a `link` in the `head` tag of your HTML:

```html
<link type="image/png" href="images/favicon.png" rel="icon">
```

Your browser will display your favicon at 16x16 pixels but it's not a bad idea to make it a little bigger as some devices are starting to use the favicon for larger bookmarking purposes. PNG and .ico files that are 32x32px or 48x48px are the best choice for favicons. (Anything under 128x128 will do just fine, just keep it square!)

## Apple Touch icons
Apple Touch icons allow you to specify the image that appears on the homescreen when someone bookmarks your website there. This means you get an app icon just like any other app!
<!-- ![Apple Touch icons on an iPhone](https://hychalknotes.s3.amazonaws.com/apple-touch-icon.png) -->

<img src="https://hychalknotes.s3.amazonaws.com/apple-touch-icon.png" alt="Apple Touch icons on an iPhone" width="300px">  

Choose an Apple Touch icon by providing a `link` in the `head` tag of your HTML:
```html
<link rel="apple-touch-icon" href="images/my-logo.png" />
```
Apple recommends that you upload an image of at least 144x144 and let the device size it down. However, you can also specify them like this as well:

```html
<!-- Standard iPhone -->
<link rel="apple-touch-icon" sizes="57x57" href="touch-icon-iphone-114.png" />
<!-- Retina iPhone -->
<link rel="apple-touch-icon" sizes="114x114" href="touch-icon-iphone-114.png" />
<!-- Standard iPad -->
<link rel="apple-touch-icon" sizes="72x72" href="touch-icon-ipad-144.png" />
<!-- Retina iPad -->
<link rel="apple-touch-icon" sizes="144x144" href="touch-icon-ipad-144.png" />
```
Services like [Iconogen](http://iconogen.com/) can create all these at once for us.

## Font Awesome

<!-- we are still using font awesome 4 to render the examples of the icons, however, the code snippets that we show students will references font awesome 5 -->
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">

Icon fonts are an amazing way to implement any number of icons easily into your website. 

Rather than downloading am image and changing the size and colour in Photoshop to use as an icon, you can embed a file of icons as a font. (Kind of like Zapf Dingbats!) From there, you can change the size and colour of the icons using CSS.

[Font Awesome](https://fontawesome.com/) is the most popular icon font, but there are many available. 

There are two ways you can embed Font Awesome on your site. 
* **CSS + web fonts**: Use the Font Awesome stylesheet and have the icons render as web fonts
* **JS + SVG**: Use the Font Awesome script files and have the icons render as SVG

Whether you choose to import the icons as a web font or as SVG, you will need to link the necessary Font Awesome files to get started. If you would like to host the files yourself you can check out [Font Awesome's documentation for `Hosting Font Awesome Yourself`](https://fontawesome.com/how-to-use/on-the-web/setup/hosting-font-awesome-yourself).

**TL;DR**: Download the files they tell you to, stick 'em in your project folder, link it in your head element.

We're not going to be downloading the files, we're going to use Font Awesome's _content delivery network_ (CDN).

### Font Awesome with web fonts and CSS
Head on over to [Font Awesome's "Get Started" page](https://fontawesome.com/get-started) and select the `Web Fonts & CSS` tab.

![Font Awesome Get Started Interface](https://hychalknotes.s3.amazonaws.com/font-awesome.png)

It's best to copy the link directly from the Font Awesome website, to ensure you have the most up-to-date link. 

To get an icon on your page, use the repurposed `<i>` tag. (Remember that it used to be used for italics?) The `<i>` tag needs two classes. These classes will be specified in the Font Awesome documentation. The first class you provide your icons will depend on the type of icons you're are using. There are 4 types available from Font Awesome. Since we're using the free version, we will only have access to the solid and brand icons.

![Font Awesome documentation of icon types](https://hychalknotes.s3.amazonaws.com/font-awesome-doc.png)

Using the Font Awesome [documentation](https://fontawesome.com/icons), add the correct icons to [this file](https://hychalknotes.s3.amazonaws.com/font-awesome-with-css.html). Then add the correct icons and make them all the right colors. Icons can be styled just like any other element.

### Font Awesome with JS and SVG
Head on over to [Font Awesome's "Get Started" page](https://fontawesome.com/get-started) and select the `JS & SVG` tab.

Download and open this file [this file](https://hychalknotes.s3.amazonaws.com/font-awesome-with-js-and-svg.html) and replace the script tag with the most current one from the Font Awesome website. Then add the correct icons and make them all the right colors. Icons can be styled just like any other element.

Note that you'll be putting the Font Awesome script in the **head** of your document.

## Accessibility and icons
Screen readers and other assistive technologies are able to read icons. Using the `aria-hidden` attribute we can define which icons should be read out and which ones should be ignored. If `aria-hidden` is set to true, screen readers will know to skip the element. If an icon is used for decorative purposes, we most likely do not want it to be read out by screen readers, so we will want to add `aria-hidden="true"` to our `i` element.

```html
<!-- Will not be read out by screen reader. The star is just a decorative element -->
<i class="fas fa-star" aria-hidden=“true”></i>
```

Sometimes we want our icons to be read out by screen readers. If your icons have semantic meaning, Font Awesome recommends that we add a few more things to make things more accessible. We need to add `aria-hidden="true"` to the icon to hide it from screen readers, and supplement it with a `span`.  What you put between the span tags will get read out by screen readers. Then we add a class of `sr-only` to the `span`. Font Awesome deals the with the styling for `sr-only` and will *visually* hide the span from users. Still with us? No? Let's check out an example:

```html
<h2>From HackerYou to Loblaws:</h2>
<i class="fas fa-walking" aria-hidden="true"></i>
<span class="sr-only">Time by walking:</span>
<p>4 minutes</p>
<i class="fas fa-bicycle" aria-hidden="true"></i>
<span class="sr-only">Time by bike:</span>
<p>1 minute</p>
```
Which will render out:  

<img src="https://hychalknotes.s3.amazonaws.com/example-font-awesome.png" alt="Example of semantic icons" width="400px">  

The walking icon and bike icon have semantic meaning. By creating the `span`, we can ensure that the icons are still accessible to users who do not benefit from the icons visually.  

Another way to make your icons accessible is using the `aria-label` attribute. This is great for interactive elements. For example, lots of sites use icons to link users to their social media. Be sure to make these icons accessible, as you want people to know they serve a purpose and are clickable:

```html
<a href="https://www.instagram.com/thisishackeryou" aria-label="Go to HackerYou's Instagram page">
  <i aria-hidden class="fab fa-instagram"></i>
</a>
```
Choose one of the files from earlier today and make the icons accessible.

Find out more from the [Font Awesome page on icon accessibility](http://fontawesome.io/accessibility/) as well as the[W3C's page on the `aria-hidden`](https://www.w3.org/WAI/PF/aria/states_and_properties#aria-hidden) attribute.