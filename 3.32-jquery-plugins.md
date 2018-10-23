## jQuery Plugins

Along with HTML and CSS for style and structure, a web page is also made up of interactions. These interactions are completed through the use of JavaScript. 

While you may not be familiar with JavaScript, there is a library called jQuery that exists to make writing JavaScript easier. Along with jQuery, there are jQuery plugins that fellow developers have created to help integrate these interactions into a site without much trouble.

Integrating a jQuery plugin into your existing code is often quite simple. The developer will provide instructions on how to install their plugin with your code.

For a large, curated collection of jQuery plugins, visit <a href="http://www.unheap.com/" target="_blank">http://www.unheap.com/</a>.

Let's take a look at how to integrate two useful jQuery plugins into our code.

For this lesson, download <a href="https://hychalknotes.s3.amazonaws.com/jqueryplugins.zip" class="exercise" download>jqueryplugins.zip</a> and open it in your text editor and browser.

#### Script tags

JavaScript comes preloaded in our browsers, however, jQuery does not. In order to use the jQuery library (which our plugins require), we have to import it into our page.

To do this, we use the `<script></script>` element. This is much like the `link` element we use for CSS. We need to provide a path to the script tag to define what file to import. We do this via the `src` attribute.

```html
<script src=""></script>
```

#### jQuery

jQuery is an open source JavaScript library that needs to be imported. We could download the library and create a separate file for it, but it's recommended that we leverage what is known as a CDN. A CDN or Content Delivery Network is a service that hosts files for developers to utilize.

Google manages a CDN that we can utilize at <a href="https://developers.google.com/speed/libraries/#jquery" target="_blank">https://developers.google.com/speed/libraries/#jquery</a>. We can visit the link and copy the script tag.

```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.0/jquery.min.js"></script>
```

#### Where to put scripts

In our index.html file, we can now import jQuery into our project. Typically, any JavaScript is loaded at the bottom of our HTML. Place the copied jQuery script tag under your content, but before the closing 'body' tag.

```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.0/jquery.min.js"></script>
</body>
</html>
```

#### Document Ready
Script tags are not just for importing javascript files. They can also be used to write JavaScript in.

With each plugin we utilize, we will need to initialize them and provide some options and settings.

**After** the script tag where you imported jQuery, create another script tag after our jQuery import. However, we do not need a `src` attribute.

```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.0/jquery.min.js"></script>
<script>
    
</script>
```

Inside of the script tags, we will provide a piece of code, that ensures the page is loaded, along with jQuery before we turn on the plugins. During the JavaScript lessons, the code will be explained further.

```html
<script>
    $(function() {

    });
</script>
```

Note: There should only ever be **one** document ready per HTML page.

## Flickity

<a href="http://flickity.metafizzy.co/" target="_blank">Flickity</a> is a powerful tool that allows us to create galleries that work on touch devices.

The documentation for Flickity is very detailed and makes it easy to understand and implement. The important part of installing a plugin is to read the documentation, often they will hold examples of how to implement.

Following the quick start, we can see that we need to include two files on our site, the jQuery plugin and the CSS go along with it. Often plugins will come with CSS that helps complete the effect.

We can find the JavaScript and CSS that we need either by downloading from the Flickity site or via a CDN.

A Google search for 'Flickity CDN' turns up the following link - <a href="https://cdnjs.com/libraries/flickity" target="_blank">https://cdnjs.com/libraries/flickity</a>. There are four links we can use here. 

- https://cdnjs.cloudflare.com/ajax/libs/flickity/1.1.2/flickity.css
- https://cdnjs.cloudflare.com/ajax/libs/flickity/1.1.2/flickity.min.css
- https://cdnjs.cloudflare.com/ajax/libs/flickity/1.1.2/flickity.pkgd.js
- https://cdnjs.cloudflare.com/ajax/libs/flickity/1.1.2/flickity.pkgd.min.js

The difference between the files is that the links with 'min' in their filename are 'minified'. That means all the unnecessary whitespace has been removed from the file, effectively making it smaller. Much more our style since we want to keep our page load size down.

#### Implementation

First, we need to load the CSS into our page. Like before, we use a link tag to load the styles into the head of our file.

```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/flickity/1.1.2/flickity.min.css">
```

Next, we need to load in the JavaScript. This will go at the bottom of our page in a very specific place. We need to use jQuery with our plugin, so our plugin needs to be loaded **after** jQuery, but before we set it up with our document ready.

```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.0/jquery.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/flickity/1.1.2/flickity.pkgd.min.js"></script>
<script>
    $(function() {

    });
</script>
```

#### Initialization
Looking at the documentation, we can initialize our plugin in a few different ways.

**HTML**

To implement in via HTML, we simply add a class of `js-flickity` to the parent element of our gallery.

```html
<div class="gallery js-flickity">
```

With that, our gallery is working.

**JavaScript**
We want to group all JavaScript together and if we want to provide any additional information to our plugin, we will muddy up the markup.

Remove the `js-flickity` class from the parent element.

In our document ready, we can select an element, and apply a _method_ called `flickity` to it.

```html
<script>
    $(function() {
        $('.gallery').flickity();
    });
</script>
```

Again, our gallery is working! The JavaScript method is preferred due to the organization.

#### Options
Our gallery has some empty areas however. jQuery plugins will offer options that can be passed in. These options are settings created by the developer, that you can provide to tweak the functionality or look.

A list of options we can provide to Flickity can be found <a href="http://flickity.metafizzy.co/options.html">here</a>. Let's explore the 'wrapAround' option.

To provide options to a plugin, we pass them into the method we applied, surrounded by curly braces.

```html
<script>
    $(function() {
        $('.gallery').flickity({
            
        });
    });
</script>
```

In the documentation for <a href="http://flickity.metafizzy.co/options.html#wraparound" target="_blank">wrapAround</a>, it states that we have to provide an option of true to turn it on. The syntax is similar to how we create CSS properties and values.

```html
<script>
    $(function() {
        $('.gallery').flickity({
            wrapAround: true
        });
    });
</script>
```

## Smooth Scroll

Smooth Scroll is a great plugin that helps to animate the browser when clicking on in-page links. Instead of the hard jump to each id, we can utilize JavaScript to perform the in-between animations.

Visit the <a href="https://github.com/kswedberg/jquery-smooth-scroll" target="_blank">Github page for Smooth Scroll</a> to follow along.

Not all documentation is super readable. Developers are under no obligation to even make documentation, as they are providing a free tool. This is the case with Smooth Scroll.

However, there are a few pieces we can see that will help us install the plugin. We already know that we require the plugin to be imported into our page.

Again, we could download the JavaScript directly, or we could leverage a CDN. A search on Google for 'Smooth Scroll CDN' turns up the following link - <a href="https://cdnjs.com/libraries/jquery-smooth-scroll" target="_blank">https://cdnjs.com/libraries/jquery-smooth-scroll</a>.

Create a new script tag **after** the jQuery script tag and set the source to the CDN link.

```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery-smooth-scroll/2.1.2/jquery.smooth-scroll.min.js"></script>
```

#### Implementation

Back on the Github page, it states the following:

"Works like this: `$('a').smoothScroll();`"

`$('a')` represents all `a` tags on the page. `.smoothScroll()` is a 'method' we are applying to them. This piece of code goes directly inside of our document ready function.

```html
<script>
    $(function() {
        $('.gallery').flickity();
        $('a').smoothScroll();
    });
</script>
```

Immediately you'll find that any links that go to 'id's are immediately scrolling!

**Options**
Plugins often offer options and Smooth Scroll is no exception. When applying Smooth Scroll to the page, we can provide options to the page.

_Available options are located <a href="https://github.com/kswedberg/jquery-smooth-scroll#options" target="_blank">here</a>_

```html
<script>
    $(function() {
        $('a').smoothScroll({
            offset: 100
        });
    });
</script>
```