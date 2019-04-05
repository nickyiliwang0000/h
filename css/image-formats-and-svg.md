<!-- Student takeaway -->
<!-- By the end of this lesson, the student should know:
- The four basic types of images files (GIF JPEG PNG SVG)
- The strengths of each file type
- What the picture element is good for (providing different images for different screen sizes/orientation)
- That they should optimize their images (e.g. compress, resize, choose the right file type)
-->

# Image formats and SVG

There are several file types used for adding images to a web page. Each type is best suited for specific kinds of images. You'll want to use the format that maintains the best quality and the smallest file size.

First, a quick look at two types of compression:   

* **Lossless:** the image is made smaller with no loss to the quality. The image can be saved over and over without losing any image clarity.
* **Lossy:** the image is made (even) smaller, but loses some of the quality. When saving an image in a lossy format repeatedly, the image quality gets progressively worse.

## GIF

The _Graphics Interchange Format_ (GIF) uses **lossless** compression, however because images saved as GIFs can only use a maximum of 256 different colours, it is best used for images with minimal colour variation to limit loss of detail. Introduced in 1987, it is one of the oldest image file types.

GIF images can also have transparency (though transparency is better handled with PNGs). And of course, they can also be animated!

**Best used for**: Images with simple colours, line drawings, icons and animations of the same.

In modern web development, they've mostly been replaced by JPEGs and SVGs.

## JPEG

The _Joint Photographic Experts Group_ format (JPEG, sometimes JPG because of [an old quirk in MS DOS](https://theydiffer.com/difference-between-jpg-and-jpeg/)) uses **lossy** compression. It can support lots of rich colours and gradients making it optimal for photographic images. It was created in 1992 by (surprise!) the Joint Photographic Experts Group.

The lossy compression makes JPEG a less favourable format for images with flat colours and line drawings. JPEGs generally have larger file sizes than GIFs.

Typically, images online are in JPEG format. We recommend using them for background images.

**Best used for**: Photographs and images with lots of rich colours and gradients.

## PNG

There are two types of _portable network graphics_ formats, PNG-8 and PNG-24. They both use **lossless** compression.  The PNG file format was created in 1995 to replace GIFs.

### PNG-8
PNG-8 is short for "8-bit PNG" because the image is 8 bits per pixel. Similar to GIFs, PNG-8 images can only store 256 colours and support transparency but they have better support for *alpha* transparency than GIFs.

![png-8 vs gif](http://i.stack.imgur.com/B09oZ.png)

PNGs **do not** support animation so stick to GIFs for that.

**Best used for**: Images with simple colours (including those that require alpha transparency).

### PNG-24

PNG-24 is short for "24-bit PNG", meaning it can hold a lot more colours than PNG-8. Just like PNG-8, PNG-24 supports alpha-transparency.

PNG-24 files are usually much bigger than JPEGs, GIFs and PNG-8s. Even though PNG-24s can handle a lot more colours, they are not meant to replace JPEGs. 

**Best used for:** Images with rich colours, gradients and shadows, that all require transparency, alpha transparency, or opaque background.

## Bitmap vs. vector

All the previous image formats mentioned here are _bitmap_ formats, which means a computer divides up the image into little squares of color. The opposite of bitmap format is _vector_ format, where the computer makes an image without those little squares and the lines are smoooooth.

![Vector vs. bitmap image from Wikipedia, via Darth_Stabro](https://en.wikipedia.org/wiki/Vector_graphics#/media/File:VectorBitmapExample.svg)

## SVG

_Scalable vector graphics_ (SVG) is a format based on XML but you can use them like other image types (e.g. in an image tag). SVGs consist of circles, rectangles, and paths created in XML. Because SVG elements are vectors (instead of bitmaps), you can apply colours, gradients, and filters to them (though not all browsers support all filter types). SVGs generally have small file sizes and scale without losing clarity or line sharpness. Because of this, look great on retina displays.

SVGs are [not supported in IE8](https://caniuse.com/#search=svg) and below.

**Best used for:** 2D shapes and icons (e. g. cartoon graphics or illustrations) and animations.

Because SVG is based on XML, it can also be added inline to an HTML document. When included inline, you can apply CSS and JavaScript to your SVGs!

### Using SVGs inline

A great thing about inline SVGs is that they remove unnecessary HTTP requests. When you define an images in an `src` attribute, you asking the browser to **request** that file from your site's server. This request will take bandwidth and time to download. SVGs embedded inline don't need to be requested using HTTP, which makes your website faster.

Screen reader support for SVGs isn't as robust as it is for other elements, so do things like adding `<title>`, `<desc>`, `aria-labelledby` and `role` attributes if there isn't already a clear label for your SVG. [More on SVG and accessibility here](https://css-tricks.com/accessible-svgs/) and [here](https://developer.paciellogroup.com/blog/2013/12/using-aria-enhance-svg-accessibility/).

#### Finding and creating SVGs

SVGs can be created using software like Adobe Illustrator or [Sketch](https://www.sketchapp.com). There are also online resources like [The Noun Project](http://thenounproject.com/) that have a wide variety of icons available for download.

But once we've found the perfect image to use, where do we actually get the SVG code that we'll put inline in our HTML document? Why, inside the SVG file's `<svg>` tags! Open the SVG file in your text editor and... there's the code.

#### The `<svg>` element
You can also create SVGs without an image editor using SVG-specific tags inside with the `<svg>` element. Note the inclusion of the two namespace declarations so the browser will read this fragment as an SVG element rather than an XML file:

```html
<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
</svg>
```

#### Basic shape elements
An `<svg>` tag can contain any of the following basic shape elements:

shape | tag
--|--
rectangle | `<rect>`
circle | `<circle>`
ellipse | `<ellipse>`
straight line | `<line>`
polyline | `<polyline>`
polygon | `<polygon>`

Each element also has different attributes used to define various styles of the shapes.

```html
    <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
        <rect x="10" y="30" height="100" width="100" style="stroke:#006600; fill: #cc0066;"/>
        <circle class="circle" cx="200" cy="80" r="30" />
        <line x1="300" y1="30" x2="300" y2="135"/>
    </svg>
```

<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" height="150" width="400">
        <rect x="10" y="30" height="100" width="100" style="stroke:#006600; fill: #cc0066;"/>
        <circle class="circle" cx="200" cy="80" r="30" />
        <line x1="300" y1="30" x2="300" y2="135"/>
    </svg>

The `x` and `y` attributes are used to determine the location of the rectangle relative to the parent element's location. The `width` and `height` attributes determine the size of the rectangle. The style attribute can also be used to set inline CSS.

The location of the circle is determined by `cx` and `cy` and has a radius of `r`.

The length and direction of the line is determine by the starting point `x1`, `y1` and the ending point `x2`, `y2`.

#### The `<path>` element

This element is used to draw advanced shapes made out of lines, arcs, and curves.

#### The `<g>` element
This element is used to group SVG shapes together so they can be treated as a single shape.

#### SVG and CSS
Styling SVG with CSS is the same as for other HTML elements. However, there are CSS properties that are specific for SVG. For example, instead of using `background` or `background-color`, `fill` will change the colour of the icon. To create a border, use the `stroke` property. 

See the [full list of SVG properties](http://www.w3.org/TR/SVG/propidx.html).

Download [inline-svg.zip](https://hychalknotes.s3.amazonaws.com/inline-svg.zip) and open it in your editor. Let's try adding images using the `<img>` tag and inline (there's a few to choose from in the `images` folder) and some CSS!

### More SVG resources
* [Using SVG](http://css-tricks.com/using-svg/)
* [Styling Scalable Vector Graphic (SVG) With CSS](http://www.hongkiat.com/blog/scalable-vector-graphic-css-styling/)
* [How to Create a Responsive SVG](http://joshuasortino.com/journal/creating-a-responsive-svg)
* [W3C SVG documentation](http://www.w3.org/TR/SVG11/expanded-toc.html)

## The `picture` element

Introduced by a group called the [Responsive Images Community Group](https://responsiveimages.org/), the `<picture>` element was designed to allow developers to art direct their pages!

The `<picture>` element can internally define multiple image sources. Usually, these images differ in size, resolution, and/or orientation. These sources have breakpoints that designate when each image should be loaded. Smaller (size, resolution) files can be loaded on smaller screens and larger ones can be loaded on larger screens. This prevents wasted bandwidth and gives a developer lots of control over the art direction of their images.

Use the `<picture>` element when you have images of different sizes, resolutions, or orientations (or any combination of those) that **are considered content**. 

### Syntax for the `picture` element

```html
<picture>
    <source srcset="imgs/large.png" media="(min-width: 980px)">
    <source srcset="imgs/medium.png" media="(min-width: 600px)">
    <img src="imgs/small.png" alt="A small picture of a thing">
</picture>
```

The `<picture>` element uses `<source>` elements inside of it to determine the images that should be loaded. The `media` attribute defines **when** those images should be displayed. Just like our `@media` blocks in CSS, the value of the `media` attribute is a condition.

You can use an `<img>` tag as a fallback if none of your conditions are met or if the browser does not support the `<picture>` element.

Let's open up [an example](https://hychalknotes.s3.amazonaws.com/picture-element-example-bootcamp.zip) and take a look.

### More `<picture>` resources
* [An example of using the `<picture>` element](https://googlechrome.github.io/samples/picture-element/) to show different images at different screen sizes.
* [A walk-through](https://www.html5rocks.com/en/tutorials/responsive/picture-element/) of the `<picture>` element


## Image formats: TL;DR

![Concise, graphic explanation of image formats](https://hychalknotes.s3.amazonaws.com/image-information-grid.png)

## Image optimization

It's important to choose the best image format and to optimize your images. There are many factors to consider when choosing images for your projects (e.g. the size and kind of the image and the user's network speed).

**Remember to:**
* Use the appropriate file type for the content of the image.
* Resize images to the dimensions you need **before** using them in a web page.
* Save images using the 'Save for web' option if you're using an image editor like Photoshop.
* Try to keep your image file sizes as small as possible (up to 400KB at an absolute maximum).

### Optimization resources

There are free applications available that can compress and otherwise optimize your images. Here are some handy tools:

* [Kraken](https://kraken.io/) an image optimizer/compressor
* [Pixlr](https://pixlr.com/), a photo editor
* [Image Optim](https://imageoptim.com/), an image compressor and "cleaner"
* [SVG Optimiser](http://petercollingridge.appspot.com/svg-optimiser), just what it says
* [Squoosh](https://squoosh.app/), an in-browser compression GUI 

Here are a few articles on image optimization:
* [How to optimize images for the web](http://johnkuefler.com/how-to-optimize-images-for-the-web)
* [10 Must Know Image Optimization Tips](http://www.shopify.ca/blog/7412852-10-must-know-image-optimization-tips)




