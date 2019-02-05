<!-- Student takeaway -->
<!-- By the end of this lesson, the student should know:
- The four basic types of images files (GIF JPEG PNG SVG)
- The strengths of each file type
- What the picture element is good for (providing different images for different screen sizes/orientation)
- That they should optimize their images (e.g. compress, resize, choose the right file type)
-->

# Image Formats

There are several file types used for adding images to a web page. Each type is best suited for specific kinds of images. As a rule of thumb, use the format that maintains the best quality while reducing the file size.

First, a quick look at two types of compression:   

* **Lossless:** the image is made smaller with no loss to the quality. The image can be saved over and over without losing any image clarity.
* **Lossy:** the image is made (even) smaller, but loses some of the quality. When saving an image in a lossy format repeatedly, the image quality gets progressively worse.

## GIF

The _Graphics Interchange Format_ (GIF) uses **lossless** compression, however because images saved as GIFs can only use a maximum of 256 different colours, it is best used for images with minimal colour variation to limit loss of detail. Introduced in 1987, it is one of the oldest image file types.

GIF images can also have transparency (though transparency is better handled with PNGs). And of course, they can also be animated!

**Best used for**: images with simple colours, line drawings, icons and animations - mostly replaced by jpgs and svgs.

## JPEG

The _Joint Photographic Experts Group_ format (JPEG) uses **lossy** compression. It can support lots of rich colours and gradients making it optimal for photographic images. It was created in 1992 by(surprise!) the Joint Photographic Experts Group.

The lossy compression makes it less favourable for images with flat colours and line drawings.  JPEGs generally have larger file sizes than GIFs.

Typically, images online are in JPEG format. We recommend using them for background images.

**Best used for**: photographs and images with lots of rich colours and gradients.

## PNG

There are two types of _portable network graphics_ formats, PNG-8 and PNG-24. They both use **lossless** compression.  The PNG file format was created in 1995 to replace GIFs.

### PNG-8
PNG-8 is short for "8-bit PNG" because the image is 8 bits per pixel. Similar to GIFs, PNG-8 images can only store 256 colours and support transparency but it have better support for *alpha* transparency than GIFs.

![png-8 vs gif](http://i.stack.imgur.com/B09oZ.png)

PNGs do not support animation so stick to GIFs for that.

**Best used for**: Images with simple colours including those that require alpha transparency.

### PNG-24

PNG-24 is short for "24-bit PNG", meaning it can hold a lot more colours than PNG-8. Just like PNG-8, PNG-24 supports alpha-transparency.

PNG-24 files are usually much bigger than JPEGs, GIFs and PNG-8s. Even though PNG-24s can handle a lot more colours, they are not meant to replace JPEGs. 

**Best used for:** Images with rich colours, gradients and shadows, that all require transparency, alpha transparency, or opaque background.

## SVG

Scalable vector graphics (SVG) are a vector graphics format based on an XML format but you can use them like other image types (e.g. in an image tag). SVGs generally have small file sizes and scale without losing clarity. They also look great on retina displays.

Because SVG is based on XML, it can also be added inline in an HTML document. When included inline, you can apply CSS and JavaScript can to your SVGs!

SVGs are not supported in IE8 and below.

**Best used for:** 2D shapes and icons (e. g. cartoon graphics or illustrations) and animations. Not good for photos.

### Using SVGs inline

SVGs consist of circles, rectangles, and paths created in XML and combined into drawings on web pages rather than in a bitmap, as other image types are. Because SVG elements aren't bitmaps, you can apply colours, gradients, and filters to them (though not all browsers support all filter types). 

A great thing about inline SVGs is that they remove unnecessary HTTP requests. When you define an images in an `src` attribute, you are defining a file that the browser will **request**. This request will take up bandwidth and require time to download. SVGs embedded inline don't need to be requested using HTTP which makes your website faster.

However, screen reader support is poor which can create a challenge for sites that use SVG where accessibility is a requirement. [More on SVG and accessibility here](http://schepers.cc/authoring-accessible-svg).

#### Finding and creating SVGs

SVGs can be created using vector graphics software such as Adobe Illustrator or [Sketch](https://www.sketchapp.com). There are also online resources like [The Noun Project](http://thenounproject.com/) that have a wide variety of icons available for download.

But once we've found the perfect image to use, where do we actually get the SVG code that we'll put in our HTML document? Why, inside the SVG file, of course! You can open an SVG file in your text editor and... there's the code.

#### SVG and CSS
Styling SVG with CSS is the same as for other HTML elements. However, there are CSS properties that are specific for SVG. For example, instead of using `background` or `background-color`, use `fill` to change the colour of the icon. To create a border, use the `stroke` property. 

See the <a href="http://www.w3.org/TR/SVG/propidx.html" target="_blank">full list of SVG properties</a>.

Download [inline-svg.zip](https://hychalknotes.s3.amazonaws.com/inline-svg.zip) and open it in your editor. Let's try adding images using the `<img>` tag and inline (there's a few to choose from in the `images` folder) and some CSS!

#### The `<svg>` element
You can also create SVGs without an image editor using SVG-specific tags starting with the `<svg>` element. Note the inclusion of the two namespace declarations so the browser will read this fragment as an SVG element rather than an XML file:

```html
<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
<svg>
```

#### Basic shape elements
SVG contains the following set of basic shape elements:

* rectangles `<rect>`
* circles `<circle>`
* ellipses `<ellipse>`
* straight lines `<line>`
* polylines `<polyline>`
* polygons `<polygon>`

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

#### The `<path>` element

This element is used to draw advanced shapes combined with lines, arcs, curves, etc., with or without fill. 

#### The `<g>` element
This element is used to group SVG shapes together. This group can then be treated as a single shape.

### Exercise
Download [the wombly path SVG exercise](https://hychalknotes.s3.amazonaws.com/wombly-path-svg-exercise.zip) and follow the notes inside. Or, for a harder challenge, open the ANSWER and code it from scratch.

### More SVG resources
* <a href="http://css-tricks.com/using-svg/" target="_blank">Using SVG</a>
* <a href="http://www.hongkiat.com/blog/scalable-vector-graphic-css-styling/" target="_blank">Styling Scalable Vector Graphic (SVG) With CSS</a>
* <a href="http://joshuasortino.com/journal/creating-a-responsive-svg" target="_blank">How to Create a Responsive SVG</a>
* <a href="http://www.w3.org/TR/SVG11/expanded-toc.html" target="_blank">W3C SVG documentation</a>

## Image Formats: TL;DR

![Concise, graphic explanation of image formats](https://hychalknotes.s3.amazonaws.com/image-information-grid.png)

## The `picture` element

Introduced by a group called the [Responsive Images Community Group](https://responsiveimages.org/), the `<picture>` element was designed to allow developers the ability to art direct their pages!

The idea is this: you have an element that internally defines many different sources. These sources have breakpoints that mean that specific images will load at specific times.

This prevents wasted bandwidth if you have a really large image for desktop, but need a smaller one for mobile.  

> The most important thing about the `<picture>` element is that **it allows you to load different versions of the image for different screen sizes.**

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

Let's try a few together to see it in action!

## Image optimization

It's important to choose the best image format and to optimize your images. There are many factors to consider when choosing images for your projects (e.g. the size and kind of the image and the user's network speed).

**Remember to:**
* Use the appropriate file type for the content of the image.
* Resize images to the dimensions you need **before** using them in a web page.
* Save images using the **save for web** option if you're using an image editor like Photoshop.
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




