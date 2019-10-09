<!-- Student takeaway: -->
<!--Student will be able to:
- Explain what responsive design is
- Identify what makes a site responsive (viewport meta tag, media queries)
- Name two common media queries (there are 4 talked about and another 5 listed in the lesson)
- Identify when to create breakpoints (when their content breaks)
- Know how to use max-width to keep content (including images) from overflowing its container
- Use the browser inspector to emulate common non-laptop devices 
-->

# Responsive design

_Responsive design_ aims to provide the best experience for whatever device a user is viewing a site on from a 27" display all the way down to a mobile phone screen.

![Screenshot of the Stripe website on 4 devices of varying sizes from mediaqueri.es](https://hychalknotes.s3.amazonaws.com/mediaqueri.es-stripe.png)

### History of Responsive Design

Previously web developers would create what were called _m dot_ sites (as in `http://m.yoursite.com`), which were a version of the desktop HTML and CSS optimized for mobile screens. This meant that developers had to create **two** independent websites and update them both when they had new content. Not very efficient!

In 2010, a developer [described one solution to these problems](https://alistapart.com/article/responsive-web-design) with the term responsive design and introduced the concept of a single codebase (e.g. one entire website) that reacts to the user's viewport. 
<!-- 
![Screenshot of the NASA website on 4 devices of varying sizes from mediaqueri.es](https://hychalknotes.s3.amazonaws.com/mediaqueri.es-nasa.png) -->

## How to make a site responsive

To make a responsive website, you need two things:
1. a special `<meta>` tag  
2. _media queries_ in your CSS

### 1. `<meta>` tag

Remember that `<meta>` tags go inside the `head` tag to provide information about the web page to the browser but not the user.

`<meta name="viewport" content="width=device-width, initial-scale=1.0">`


<!-- 
* `meta` is the name of the tag.
* `viewport` is the value of the `name` attribute. It specifies what this `meta` tag applies to.
* `content` is where we provide the information about the viewport. We provide as many key-value pairs as we want here, each comma separated.
* `width=device-width` tells the browser how wide the website should be. We can set this to an explicit pixel value but because that value varies by device, we use the `device-width` keyword to tell the browser that this site should be as wide as the device it is loaded on.
* `initial scale` is how much the site is zoomed in or out by default. A value of 1.0 will render the size just as it is, no zoom in or out. A value of 0.5 would zoom it out while 1.5 would zoom it in.
* `user-scalable=no` (not shown in tag above), is how we can keep users from zooming. This could be used if providing a mobile-optimized experience and zooming/panning is not required.
* `minimum-scale` and `maximum-scale` is how we can limit how much a user is allowed to scale (e.g. these could be set to .5 and 2 respectively). -->


You should **always** put this tag into the `head` of your document. Add it as a snippet to your code editor! Without this tag, your site **will not be responsive**. It will render as a shrunk down version of your desktop site. 

### 2. Media queries

Once you've added the viewport tag, _media queries_ are what actually make your site responsive. Media queries are conditional statements for your CSS that start with the `@media` keyword.

```css
@media (max-width: 940px) {
  body {
    background:red;
  }
}
```

This media query is saying "for all media, up until the screen is 940px wide, the background of the body is red."

If we have more than one rule it would look like this:

```css
@media (max-width: 940px) {
  body {
    background:red;
  }
  h2 {
    font-size:20px;
  }
}
```

The first pixel value here is what we call a _breakpoint_. Breakpoints are the conditions under which a certain set of CSS rules are applied. An easy way to visualize breakpoints in development is to set a background color on the body to make it obvious which breakpoint you are in.

Open [media-queries-1.html](https://hychalknotes.s3.amazonaws.com/media-queries--bootcamp.html) in your editor and browser and let's take a look through the code.

Dev tools has introduced a ruler that shows you pixel values. You can use that or inspect the body of your page to get the current page width and height.

#### Min and Max Width in Media queries

The most common media queries target the width of a device.

```css
@media (max-width: 940px) {
  body {
    background:red;
  }
}
```

The above example designates **only** a `max-width`, which means that the rule applies to every screen width below that. There is also a `min-width` media query which means that the rule applies to every screen width above that. 

```css
@media (min-width: 1240px) {
  body {
    background: blue;
  }
}
```

Sometimes we will want to limit our CSS to a certain range of pixel values:

```css
  /* Portrait tablet to landscape and desktop */
  @media (min-width: 768px) and (max-width: 940px) { }
```

The code between the curly brackets will only be run when the width of your browser is equal to or greater than 768px **and** less than or equal to 940px.

These bounded media queries can be helpful when you are targeting a specific size of screen. If, however, you want your CSS to apply to every screen size below the one targeted, leave out the `min-width` like we did in our first example. 

#### Mobile First Design

Change all the media queries from `max-width` to `min-width`. How does that change the order of the background colors? 

You may hear the phrase _mobile-first design_ which means pretty much what it sounds like: your base CSS will be the mobile styling. Therefore, you will mostly use `min-width` media queries because you are watching for where the mobile styles no longer look good. The opposite approach (it doesn't have a catchy name) assumes that the base CSS is for the desktop site and as it get smaller (or larger, but mostly smaller), new rules will have to be introduced -  then you'll use `max-width` to target smaller.

Download this [width-media-queries-exercise.zip](https://hychalknotes.s3.amazonaws.com/width-media-queries-exercise.zip) to see how you can acheive the same look with mobile-first or desktop-first media queries.


#### Media query for height

Occasionally you may want to check if a device has a certain height.

Imagine that you have a header set to `height: 100vh` with a long title inside of it. On phones with short screens or small tablets in landscape mode the title might get cut off or break out of its container. 

Download [height-mq.html](https://hychalknotes.s3.amazonaws.com/height-mq.html) to see this issue in action. Open it in the device emulator on a small phone. See how the text runs past the image? We can solve this issue by having the header automatically size itself to its contents once the screen is below a certain height:

```css
header {
  height: 100vh;
  /* For most screens with enough height to contain the content */
}

@media (max-height: 600px) {
  header {
    height: auto;
    /* For screens under 600px */
  }
}
```

If the issue applies when the screen is narrow but longer than a phone screen, you can also combine a media query for height and one for width: 

```css
 @media (max-height: 800px) and (max-width: 450px) {
  header {
    height: auto;
  }
}
```

**You shouldn't rely on height media queries** for much beyond cases like the one above! Using height media queries for design decisions is tricky and unreliable, because browser heights are even more unpredictable than widths. Some things to note:

  * A phone's browser bar takes up height and there's generally a context menu at the bottom of a phone screen.
  * People may be viewing your site from an in-app browser (e.g. from Facebook or Twitter).
  * Some people use Google Chrome on the iPhone which takes up a different amount of vertical height than Safari.

Trying to target a specific device is not a good idea: you are better off using width media queries most of the time.

#### Other Media Queries
  * **orientation**: Thinking about **why** the user is holding their phone at that particular orientation may help you make decisions about design. [More Info](https://www.smashingmagazine.com/2012/08/towards-retina-web/)
  * **pixel-density**: Images and graphics are blown up to 2x their natural size on retina or HPDI screens which can result in blurry images. The solution to this issue is to use a device resolution media query to swap in images that are 2x the size of the normal ones when the user is on a HiDPI screen. [More Info](https://www.smashingmagazine.com/2012/08/towards-retina-web/)
  * **print**: when someone prints a web page, your `@media (print)` CSS rules can remove pieces that aren't needed.
  * **monochrome**: targets monochrome screens (like Kindles)
  * **progressive scan**: important pretty much only if you are making TV web apps
  * **color**: if you could somehow get a web browser on an old gameboy color, you could target low or no bits of color.
  ```css
  @media all and (color:0) and (width:160px) and (height:144px) {
    /* Target original gameboy */ 
  }
  ```

There are a bunch more on [MDN](https://developer.mozilla.org/en-US/docs/CSS/Media_queries).

### How to use breakpoints effectively

In general, we won't create breakpoints based on specific devices. There are hundreds of screen sizes out there now and more to come. What we **will** do is create them based on the design and content of our websites. (For edge cases where you absolutely **must** target specific devices, check out [this resource by Chris Coyier](https://css-tricks.com/snippets/css/media-queries-for-standard-devices/) which provides media queries for some known devices sizes.) 

In the broadest sense, the following breakpoints correspond to general device sizes:
```css
/* Portrait tablet and small desktops */
@media (max-width: 940px) {
}

/* Landscape phone to portrait tablet */
@media (max-width: 768px) {
}

/* Landscape phones and down */
@media (max-width: 480px) {
}
```

As you design your site, you may need breakpoints that are larger, smaller, or in between some of these. That's fine! We want you to always **create breakpoints based on your design/content.**
  

### Holistic Coding when creating Responsive Design

Media queries allow us to make changes at certain break points but that doesn't get us all the way to a responsive design. Let's talk about the ways that we can incorporate responsive design into the structure of our code. 

#### Layouts and Wrappers

Percentage widths on your elements and flexbox are gonna be your good pals when creating responsive layouts, but even they can't do **all** the work.

Download [responsive2.html](https://hychalknotes.s3.amazonaws.com/responsive2.html) and zoom all the way out on your dev tools (`cmd + - ` Mac and `ctrl + -` on Windows) to emulate a very wide screen - an external monitor, perhaps. See how all the content gets unreadably streeeeeeeeeeetched?

To keep it contained, add a fixed pixel `max-width` property to the wrapper. Like so:

```css
.wrapper {
  width:70%;
  margin: 0 auto;
  max-width:960px;
}
```

This allows the wrapper to be any size up to this value.

#### Scaling images within their parent containers

It's pretty common for big, beautiful desktop images to be way too large for small screens. 
<!-- 
![screenshot of an image staying within its browser](https://hychalknotes.s3.amazonaws.com/image-within-container.png) -->

<!-- 
![screenshot of an image breaking out of its container in a browser](https://hychalknotes.s3.amazonaws.com/image-breaking-out-of-container.png) -->

Open up [responsiveImages.html](https://hychalknotes.s3.amazonaws.com/responsiveImages.html) to get an idea of this issue.

When an image renders on a page, by default it starts at it's original pixel width. It doesn't care how big it's parent container is or how wide the browser window is. It will continue to render at the size that it started as unless we specify otherwise.

The fix is easy. We apply `max-width:100%;` to all images. This ensures that images are never larger than their parent elements.

```css
img {
  max-width: 100%;
}
```

Now try changing the size of the browser window. 

## Responsive testing

It's ideal to test on an actual device because, as mentioned, the predicted size of a device screen and the actual size (and resolution) said screen can be different. But to get a general sense of the responsiveness of your site, you can drag the edge of your browser to emulate phone screen sizes or use the device emulator in your dev tools:

* Dock your dev tools to the right of the screen (or in a new window completely). Click the three dots in the top right of your dev tools and select the option you want.

  ![screencap of the dev tools location menu on Firefox](https://hychalknotes.s3.amazonaws.com/dev-tools-location-menu.png)

* To get to the device emulator in your browser, click the screens icon next to the three dots.

  ![screencap of the dev tools emulator icon on Firefox](https://hychalknotes.s3.amazonaws.com/dev-tools-emulator.png)

* Turn on developer mode in Safari and use the same tools there.

  ![screencap showing how to turn on developer mode in Safari](https://hychalknotes.s3.amazonaws.com/developer-mode-safari.png)
  ![screencap of how to turn on responsive design mode in Safari](https://hychalknotes.s3.amazonaws.com/responsive-design-mode-safari.png)
  
* Go to the 'Responsive' tab in the top left of the device emulator and select 'Edit List' and you can add known or custom devices to your emulator.
* Under the settings cog in the top right, select 'Reload when user agent is changed' to reload the page when a different device is chosen.

## Code along

Download [mediaQueriesCodeAlong.zip](https://hychalknotes.s3.amazonaws.com/mediaQueriesCodeAlong--bootcamp.zip) and we can apply media queries to a desktop website and make it responsive!

## Exercises

### Responsive navigation with float
Let's try making a navigation responsive. Download the [navigation-float](https://hychalknotes.s3.amazonaws.com/navigation-float.zip) and make it responsive! Check out the answer key in your browser to see what it's supposed to look like.

### More exercises
Check out [responsive-exercises-roundup.zip](https://hychalknotes.s3.amazonaws.com/responsive-exercises-roundup+2.zip) for the exercises and answers.



<!-- 
#### More Media Queries

These are used less often, but might be fun: 
  * **color**: if you could somehow get a web browser on an old gameboy color, you could target low or no bits of color.
  ```css
  @media all and (color:0) and (width:160px) and (height:144px) {
    /* Target original gameboy */ 
  }
  ```

  * **print**: when someone prints a web page, your `@media (print)` CSS rules can remove pieces that aren't needed.
  * **monochrome**: targets monochrome screens (like Kindles)
  * **progressive scan**: important pretty much only if you are making TV web apps
  * **mac theme,windows theme**: targets specific themes on Mac or Windows -->





<!-- ## Helpful patterns
There are a lot of common patterns and problems that you will find when it comes to creating a responsive site. There is a great resource from Brad Frost called [Responsive Patterns](https://bradfrost.github.io/this-is-responsive/patterns.html) that has a lot of great examples and code for common issues. -->


