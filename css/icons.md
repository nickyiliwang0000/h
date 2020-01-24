<!-- Student takeaway -->
<!-- By the end of this lesson, the student should know:
- What a favicon is
- The optimal dimensions for favicons and Apple Touch icons
- How to use Font Awesome
- How to make a Font Awesome icon accessible
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
<link rel="apple-touch-icon" sizes="57x57" href="touch-icon-iphone-57.png" />
<!-- Retina iPhone -->
<link rel="apple-touch-icon" sizes="114x114" href="touch-icon-iphone-114.png" />
<!-- Standard iPad -->
<link rel="apple-touch-icon" sizes="72x72" href="touch-icon-ipad-72.png" />
<!-- Retina iPad -->
<link rel="apple-touch-icon" sizes="144x144" href="touch-icon-ipad-144.png" />
```
Services like [Iconogen](http://iconogen.com/) can create all these at once for us.

## Font Awesome

<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">

Icon fonts are way to implement any number of icons into your website. Rather than downloading am image and changing the size and colour in Photoshop to use as an icon, you can embed a file of icons as a font. (Kind of like Zapf Dingbats!) From there, you can change the size and colour of the icons using CSS.

[Font Awesome](https://fontawesome.com/) is the most popular icon font, but there are many available. 

You will need to link the necessary Font Awesome files to get started. The best way to find the current directions for using Font Awesome is to check [Font Awesome's "Get Started" page](https://fontawesome.com/start).

### Using Font Awesome in your Code

To get an icon on your page, use the repurposed `<i>` tag. (Remember that it used to be used for italics?) The `<i>` tag needs two classes. These classes will be specified in the Font Awesome documentation. The first class you provide your icons will depend on the type of icons you're are using. There are four types available from Font Awesome. Since we're using the free version, we will only have access to the solid and brand icons.

![Font Awesome documentation of icon types](https://hychalknotes.s3.amazonaws.com/font-awesome-doc.png)

## Exercise

Using the Font Awesome [documentation](https://fontawesome.com/icons), add the correct icons to [this file](https://hychalknotes.s3.amazonaws.com/font-awesome-with-css--bootcamp.zip) and change their colors. Icons can be styled just like any other element.

## Accessibility and icons
Screen readers and other assistive technologies are able to read icons. Using the `aria-hidden` attribute we can define which icons should be read out and which ones should be ignored. If `aria-hidden` is set to true, screen readers will know to skip the element. If an icon is used for decorative purposes, we most likely do not want it to be read out by screen readers, so we will want to add `aria-hidden="true"` to our `i` element.

```html
<!-- Will not be read out by screen reader. The star is just a decorative element -->
<i class="fas fa-star" aria-hidden="true"></i>
```

Sometimes we want our icons to be read out by screen readers. If your icons have semantic meaning, Font Awesome recommends adding a few more things to make your icons more accessible. We need to add `aria-hidden="true"` to the icon to hide it from screen readers, and supplement it with a `span`.  What you put between the span tags will get read out by screen readers. Then we add a class of `sr-only` to the `span`. Font Awesome deals the with the styling for `sr-only` and will **visually** hide the span from users. Still with us? No? Let's check out an example:

```html
<h2>From Juno to Loblaws:</h2>
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
<a href="https://www.instagram.com/junocollege" aria-label="Go to Juno College's Instagram page">
  <i aria-hidden class="fab fa-instagram"></i>
</a>
```
Choose one of the files from earlier today and make the icons accessible.

Find out more from the [Font Awesome page on icon accessibility](http://fontawesome.io/accessibility/) as well as the [W3C's page on the `aria-hidden`](https://www.w3.org/WAI/PF/aria/states_and_properties#aria-hidden) attribute.
