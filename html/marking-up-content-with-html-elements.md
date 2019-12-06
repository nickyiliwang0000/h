# Marking up content with HTML elements

## HTML: The makeup of markup

_Hyper Text Markup Language_ (HTML) is the standard language that we use to create web pages. When we open an HTML file within a browser, the code is interpreted as a visual (or audible) web page.

Think of HTML as the frame of a building. It's the structure that holds the whole thing up. HTML gives us a way to create semantic structure for the content on our web page.

When we write a text document, we might organize our content using headers, paragraphs, quotes, and lists. In HTML, we do the same. However, while we might bold or underline a header in a regular document, this is **not** something we do in HTML. That's what CSS is for. If you remember nothing else, remember that **HTML should only be used to show the structure and content of a web page**. 

### Creating a new web page

All web pages include a standard base structure. This structure will be different based on the project and age of the web page.

The current standard page structure is below:

### Base web page structure

```html
<!DOCTYPE html>
<html>
  <head>
    <title>My First Website</title>
  </head>
  <body>

  </body>
</html>
```

You can view this in your browser or code editor by downloading [hello-world.html](https://hychalknotes.s3.amazonaws.com/hello-world.html). To download the file rather than having it open in a new tab, make sure you right-click and 'Save link as...'

The base structure of a web page is something that you will not be expected to type by hand, but it's important to become familiar with it and understand what each portion of the code does.

This structure should be included on every web page.

* `<!DOCTYPE html>`
  * The `doctype` tag defines the version of HTML we are using to create our web page. In the past, this was a long tag with many keywords passed in, but with the advent of HTML5, we can use this shortened version.
* `<html></html>`
  * The `html` element is the master containing element of our web pages. We write all HTML elements and content within.
* `<head></head>`
  * The `head` element is where we provide information about the web page to the browser. No content that is meant to appear on the page actually goes in the head.
* `<title></title>`
  * The `title` element is used to define a title that will appear in the browser tab.
* `<body></body>`
  * All content that will appear in the browser is written within the body element. Typographical content and structural elements go within.

### Nesting
When you are nesting tags within each other, you must **always** close them in the reverse order that you opened them. Failing to do so will cause your HTML be to invalid. While many browsers will be forgiving and render what they **think** you probably wanted, this can cause unexpected errors further into development. Check your code editor for squiggly underlines or weird-colored text.

**👎 Incorrect:**
```html
<div>
  <h1>Welcome to the future!</h1>
    <p>Today is <strong>September 1st, 3018.
    </p>
  </div>
</strong>
```
In this example, the `</p>`, `</div>` and `</strong>` tags are closed in the wrong order. Because the `<div>` was the **first** element to be opened, it needs to be the **last** element closed.

**👍 Correct:**
```html
<div>
  <h1>Welcome to the future!</h1>
  <p>Today is <strong>September 1st</strong>, 3018.</p>
</div>
```

### HTML Comments
Comments are used to make your code more readable by future-you or another person.

Anything between `<!--` and `-->` will be commented out. You can type those characters or use the shortcuts `cmd` + `/` (Mac) or `ctrl` + `/` (PC).

```html
<!-- This is a basic comment -->
<!--
  This is a
  multi-line
  comment
-->
```

One way to make your code more readable is to use comments to mark which elements certain closing tags belong to. This can be very helpful when your page is hundreds of lines long.

```html
<header class="main-header">
  <div class="wrapper">
    <nav class="main-nav"></nav>
  </div><!-- /.wrapper -->
</header><!-- /.main-header -->

```

Another way is to mark where content starts and stops:

```html
<!-- Header code STARTS -->
  My HTML Code...
<!-- Header code ENDS -->
```
You can also use comments during development if you want to temporarily remove a section of content from view in the browser.

```html
<!-- <p>This is some <strong>content</strong> that I don't want to see on the site right now.</p> -->
```

## HTML elements

### Classic elements

#### Heading tags
A web page is made up of blocks of content. Each content section will have a heading that denotes the content's place in the page hierarchy. 

Think of your HTML document as a research paper. You would probably have a heading at the top of the page with the paper's name on it. In an HTML document, you would make that clear like this - `<h1>Paper Title</h1>`. Note that any HTML page should only have one `h1`. 

In the research paper, you may divide the paper into several high-level sections. These would be `<h2>High Level Section Title</h2>` and `<h2>Other High Level Section Title</h2>` and so on.

Under each of those sections, you would probably have a few more smaller sections (e.g. `<h3></h3>`) and so on through to `<h6></h6>`.

Browsers will style the headings by default. When you're writing your tags, **choose the tag that makes the most sense semantically**, not the one that looks most like your design.

Correctly tagged headings like this:
```html
<h1>Title of my website</h1>
<h2>Title of a high-level section of my website</h2>
<h3>Title of a less important section of my website</h3>
<h4>Title of a section in the sidebar</h4>
<h5>Title of a section in the footer</h5>
<h6>Title of a secondary section in the footer</h6>
```
Will render like this:
<h1>Title of my website</h1>
<h2>Title of a high-level section of my website</h2>
<h3>Title of a less important section of my website</h3>
<h4>Title of a section in the sidebar</h4>
<h5>Title of a section in the footer</h5>
<h6>Title of a secondary section in the footer</h6>

Use CSS to override the default styling while keeping your page's hierarchy intact.

#### Paragraph tags

The paragraph tag is one of the most frequently used tags on the internet because most of the content on the web is text. It's fairly easy to use: Every time you have a full line break in your text, wrap that entire block of text in a `<p></p>` tag. Let's use the following block of text as an example:

```html
I'm interested in design, development, and business. I've been very fortunate to be able to do all three as a career.

From a technical standpoint, I spend most of my time working with JavaScript, CSS3, HTML5, and React.js. For over 5 years, my title has been (junior, intermediate, and now senior) front-end developer. During the past year I have been working with NodeJS and SVG animations. New and open source web technologies make me super excited and I can't wait to see what's new for the web in the next few years.

I learn from the community and love to share what I have learned.
```

You can see that there are three paragraphs in this block of text. In an HTML document, we'd mark it up like this:

```html
<p>I'm interested in design, development, and business. I've been very fortunate to be able to do all three as a career.</p>

<p>From a technical standpoint, I spend most of my time working with JavaScript, CSS3, HTML5, and React.js. For over 5 years, my title has been (junior, intermediate, and now senior) front-end developer. During the past year I have been working with NodeJS and SVG animations. New and open source web technologies make me super excited and I can't wait to see what's new for the web in the next few years.</p>

<p>I learn from the community and love to share what I have learned.</p>
```

#### `strong` and `em` tags

In the past, developers used the `<b>` tag or the `<i>` tag to designate important content or content that needs extra emphasis.

Today, `<strong></strong>` and `<em></em>` tags are used to wrap content that is important or should be emphasized. Default styling in the browser bolds and italicizes them respectively. These tags are used within higher level block text elements such as heading tags or `p` tags.

##### When to use `<strong></strong>`
Use a `<strong>` tag when you want the browser to know that the enclosed text is important.
```html
<p>Driving at night can be <strong>dangerous</strong>.</p>
```
This renders:
<p>Driving at night can be <strong>dangerous</strong>.</p>

##### When to use `<em></em>`
Use an `<em>` tag to highlight or emphasize part of your content. 
```html
<p>We <em>had</em> to be there by 10.<p>
 ```
This renders:
<p>We <em>had</em> to be there by 10.<p>

The `<i>` and `<b>` tags are not completely gone. They still render bold and italic in most browsers and `<i>` has been repurposed by systems like [Font Awesome](http://fortawesome.github.io/Font-Awesome/) to represent an icon.

#### `span` tags
Spans are small but mighty HTML tags. They're **inline elements** which means that you can pop one right in the middle of a block element (like a `<p>`) and it won't give you a line break or any other unwanted effect.

Create an HTML file or follow along with [this CodePen](https://codepen.io/CoderOfNote/pen/QPxXEQ?editors=1100) that contains this sentence:

> There are lots of colors I like: red, blue, purple, green to name a few.

Suppose we wanted to visually highlight some of the words. Since this particular visual highlight is just for fun and has nothing to do with importance or emphasis, we'll use a `<span>`. 

We would first wrap our sentence in a paragraph tag:

```html
<p>There are lots of colors I like: red, blue, purple, green to name a few.</p>
```

Then we wrap the word(s) we want to target in a `span` tag and give that `span` tag a class of `contains-red`. We use a class so we can target only these **specific** `span` tags with CSS.

```html
<p>There are lots of colors I like: <span class="contains-red">red</span>, blue, <span class="contains-purple">purple</span>, green to name a few.</p>

```

#### `div` tags
The HTML document division element is used to define an area of content. In web page designs, the content is visually broken up into chunks that sometimes don't correspond to the elements available to developers. The `<div></div>` element can be used to wrap other content elements and make them available to styling as a group.

```html
<div>
  <h1>I'm the header</h1>
  <p>Cras mattis consectetur purus sit amet fermentum. Praesent commodo cursus magna, vel scelerisque nisl consectetur et. Duis mollis, est non commodo luctus, nisi erat porttitor ligula, eget lacinia odio sem nec elit. Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor.</p>
</div>
```

<!-- <note> -->

##### `div` or `span`?!!?!?!
This can be a big source of confusion — when do we use `div` and when do we use `span`? What's the difference?

The technical difference between the two is that `div` is a block element and `span` is an inline element. Now these probably don't mean much to you right now, so let's take a look at the previous example using `div` instead of `span`:

```html
<p>There are lots of colors I like: <div class="contains-red">red</div>, blue, <div class="contains-purple">purple</div>, green to name a few.</p>

```

Why does each item break on to a new line? Because `div` is a block element, which means it should not be used **in a line** or **inline**.

In general, spans go inside other elements — such as `<p>` or `<h2>` — so we can later specifically target that bit of content. `div`s are used to wrap sections of content together.


#### Image tags
The `<img>` tag is used to embed images on your web page. It has two mandatory *attributes*:

* `src`: This is the source of the image that is to appear
* `alt`: This is the alternate text that describes the image to people who can't see images or search engine robots (who also can't see images... yet)

The image's source path can be _absolute_ or _relative_.

An **absolute** image path is typically an image hosted elsewhere on the Internet. An example would be to use an image sourced via Google Image Search or from an image placeholder service like placebear.com.

A **relative** image path is one that uses your document (probably an index.html file) as a starting point. This will be a path that leads out of your document, through folders or subfolders, and ends up at the image file.

```html
<!-- using a url relative to the HTML page -->
<img src="images/dog.jpg" alt="My dog Hugo">

<!-- using an absolute url from another website -->
<img src="http://dogpictures.com/dog.jpg" alt="Someone else's dog">
```

##### Descriptive alt attributes
It's important to include alternative text in the alt attribute for all image elements. We can make the experience for those using screen readers, or those with slow internet connections, waaaaaaay better by being descriptive. Instead of `alt="my cat"`, describe the picture as you would to someone who can't see it: `alt="My cat, Chloe, stretching in a ray of sunshine beside a window"`. Descriptive alt tags can make or break a user's experience.

##### What if I don't think my image adds value?
<p>There are times when you don't need alt text. If the image doesn't add value or isn't useful to people using screen readers (maybe the picture is decorative or it's a graph whose values are discussed completely in the following text), include the alt attribute, but leave it empty, <code>img src="images/image.jpg" alt=""</code>. If you do not include a value for the alt attribute, screen readers know to skip describing the image. If you don't include an alt attribute, the image's file path will be read instead.</p>

##### Title vs alt
<p>Another common question is "When should we be using `title` attributes?". Title attributes create a tooltip on hover. Title attributes are used <strong> with an image element</strong>, whereas the alt attribute shows <strong>instead of an img element</strong>. Use both and you'll never go wrong.</p> 

##### Words in images
<p>It's better to use actual text instead of images with text in them. Screen readers can’t read the text in images, they can only read alt text on the <code>img</code> element. Also, when images with text are zoomed, they can lose readability and become pixelated. </p>
</div>

##### Place kittens and pug holders

One of the many fun parts of being a web developer is using funny images as placeholders. In many of our examples, we will use random images that we found online. Sometimes a design will require a specific size of the image; instead of finding a funny image and using photo editing software or inline styling to resize it, we can make use of services that provide placeholder images.

Here are a few options:

* [http://placekitten.com/](http://placekitten.com/)
* [https://lorempixel.com/](https://lorempixel.com/)
* [https://picsum.photos/](https://picsum.photos/)
* [https://dummyimage.com/](https://dummyimage.com/)
* [http://placeimg.com/](http://placeimg.com/)
* [https://placebear.com/](https://placebear.com/)

For each of the above, instead of setting the image src to URL that ends in an file extension that designates an image (like `.png, .jpg, .png, .jpeg, .gif`), we set it to one of the previous URLs with the last two numbers being the `width` and the `height`:

```html
<img src="https://picsum.photos/350/150">
```

<img src="https://picsum.photos/350/150">

```html
<img src="https://placebear.com/200/300">
```

<img src="https://placebear.com/200/300">

```html
<img src="http://placeimg.com/640/480/arch">
```

<img src="http://placeimg.com/340/280/arch">


#### Lists
There are two types of lists: **ordered lists** and **unordered lists**.

```html
<ol>
  <li>One</li>
  <li>Two</li>
  <li>Three</li>
</ol>

<ul>
  <li>Milk</li>
  <li>Bread</li>
  <li>Eggs</li>
</ul>
```

The only direct children that lists can have are list items: `<li></li> `.

Anything can be nested inside list items, including inline elements, block elements, and inline-block elements.

There are three main CSS properties that we can use to style lists:
1. list-style-type
2. list-style-position
3. list-style-image

The CSS shorthand for all these properties is `list-style`.

 <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/list-style">Check out the `list-style` details on MDN.</a>

Many elements on a website are semantically lists but don't look like lists in the final design. Lists have quite a bit of default styling attached to them in the browser.  To override the default styling of lists, make sure you remove the margin and the padding and set the `list-style` to none.

```css
ul, li {
  margin: 0;
  padding: 0;
  list-style: none;
}
```

#### Anchor tags (also known as links)
If you've ever made a website, chances are you've used an anchor tag.  Anchor tags (also called links, link tags, or anchor links) allow us to create a path to another web page or to places within our site.

Anchor tags have an `href` attribute which tells the browser where the user will go when the anchor tag is clicked. Here are a few examples:

```html
  <!-- Links to other sites -->
  <a href="http://google.com">Search on Google</a>
  <a href="https://junocollege.com">Visit the Juno College site!</a>

  <!-- Links within our website -->
  <a href="about.html">Visit my about page</a>

  <!--linking a nested image to another page -->
  <a href="contact.html">
    <img src="images/contact.png" alt="">
  </a>
```

> **Accessibility tip**
>
> Do not rely on something like "click here" for your link content. Using descriptive link text is important to explain context to assistive technologies. 


#### Table tags
Table tags used to be how everyone laid out their web pages.
* `<table>` : containing element for a table
* `<tr>`: Table row, holds as many `<th>` or`<td>` tags as the information requires.
* `<th>`: The table header cell tag should contain a single piece of column header information.

**👎 Incorrect:**
```html
<table>
  <tr>
  <th>Sizes Colors Stock</th>
  </tr>
</table>
```

**👍 Correct:**
```html
<table>
  <tr>
    <th>Sizes</th> 
    <th>Colors</th> 
    <th>Stock</th>
  </tr>
</table>
```
* `<td>`: The table data tag should contain a single piece of data.

**👍 Correct:**
```html
<table>
  <tr>
    <th>Date</th>
    <th>Event</th>
    <th>Venue</th>
  </tr>
  <tr>
    <td>17 March</td>
    <td>Demo Night!</td>
    <td>Juno Main Classroom</td>
  </tr>
  <tr>
    <td>19 March</td>
    <td>Industry Day</td>
    <td>Juno Main Space</td>
  </tr>
</table>
```


### Attributes
So far we've explored how we use elements to define our content and structure. Before we move into understanding how to add more content and action to our websites, we need to talk about using attributes to provide information about our elements to the browser.

An attribute exists as a declaration within the opening tag of an element and provides a value through an equals sign.

```html
<img src="images/excellentImage.png" alt="Tony Hawk doing a kick flip." />
```

In the example above, there is a `img` element that has a `src` attribute. The value of the `src` attribute is `images/excellentImage.png`. 

Different elements require different types of attributes. We already saw  `src`,`href` and `alt`. Here are some other common ones you will be using:

#### Class

The class attribute can be applied to any element. We use CSS to target classes (and by extension, elements) and apply styles to them.

The value passed into the attribute is what is known as a _class name_ and should be descriptive. Within a page, you can use any given class name on as many elements as you want. Keep in mind that there are conventions for writing class names - we will discuss these in a later lesson.

```html
<div class="banner">
    <h1>Welcome to Juno!</h1>
</div>
<header>
  <h2 class="sectionHeaderText">Isn't HTML the best?</h2>
  <h2 class="sectionHeaderText">This part is about attributes!</h2>
</header>
```

#### ID

Like the `class` attribute, the `id` attribute can be used to target an element. Unlike the `class` attribute, elements cannot share IDs. 

**👎 Incorrect:**
```html
<header>
  <h1 id="title" class="movie-name">Lord Of The Rings</h1>
  <h2 id="title" class="movie-name">The Two Towers</h2>
</header>
```

**👍 Correct:**
```html
<header>
  <h1 id="title" class="movie-name">Lord Of The Rings</h1>
  <h2 id="subtitle" class="movie-name">The Two Towers</h2>
</header>
```
An `id` is meant to identify a unique element. 

#### title
The title attribute provides more information about an element when a user hovers over it. As mentioned earlier on this page, it is best used on an image element to provide information about the image to the user.

```html
<div title="I say hello">
    <p>You say goodbye</p>
</div>
```

<div title="I say hello">
    <p>You say goodbye</p>
</div>

#### src
The `src` attribute is used to pass in the source of an element. It is most commonly used on an image element:

```html
<img src="images/dog.jpg" alt="Small beige pug wearing a Santa hat" />
```

#### href
The `href` attribute stands for *hypertext reference* and is used in anchor links.  The value of the `href` attribute is the path to where the link should take the user.

```html
<a href="https://www.junocollege.com">Juno College</a>
```

#### alt  
The alternate text that describes an image. Helpful for both search engines and visually impaired users. It is important to provide a meaningful description for your alt attribute. [Here is a great article that explains best practices for alt text](https://moz.com/learn/seo/alt-text).

The link below will bring you to the section of the page with an `id` attribute of `Markup`. And yes, capitalization matters!

<a href="http://en.wikipedia.org/wiki/HTML#Markup" target="_blank">http://en.wikipedia.org/wiki/HTML#Markup</a>

#### All the rest
We will run into many more attributes as we work with HTML. `type=" "`,`value=" "`,`placeholder=" "`,`style=" "`, `checked=" "`, `for=" "`, `name=" "`, `tel=" "` to name a few.

In your travels around the Internet, you may see some attributes from older versions of HTML that you should **never** use.  They are presented here as apocryphal reference:

* `width=" "` 
* `height=" "` 
* `align=" "`
* `color=" "`
* `size=" "`
* `bgcolor=" "`
* `font=" "`

As you may have guessed, these are all presentational. Any of these will work in the browser, but remember that when writing modern, semantic code **styling is never HTML's job**. 



#### Using attributes with anchor tags
Have you ever seen a URL that that looks like this?:

```html
http://mysite.com/about.html#food
```

When you visit it, it magically brings you to the food section of mysite.com! How does it *know*?

That octothorp (hashtag, hash symbol) designates an element's `id`. Because IDs are unique, they are the perfect thing to target when we want to move somewhere in our current page.

Let's say we have an `h2` element with an `id` of `food` in a document called `about.html`:

```html
<h2 id="food">Foods I Like</h2>
```

Inside `about.html`, we can create a link to that `id`.

```html
<a href="#food">See Foods I Like</a>
```

If we are on another page (say, `contact.html`) and want to link to that specific spot on the `about.html` page, we add that page to the href path:

```html
<a href="about.html#food">See Foods I Like (on another page)</a>
```

You can link to any element that has an ID (e.g. `<div>`, `<span>` or `<blockquote>`) but usually it'll be a heading.

Open up <a href="https://hychalknotes.s3.amazonaws.com/link-within.zip" class="exercise" download>**link-within.zip**</a> and create a navigation based on the available markup. It can be a single level navigation - no dropdowns required.

#### Creating a multipage site

All we need to do to create a multipage site is create more HTML files! We will have a main html file, usually called `index.html`, and another HTML file called `about.html`.

Within our `index.html`, we'll have a link to the `about.html` page. Like so:

```html
<!-- Inside index.html -->
<a href="about.html">About</a>
```

Bam! You've built a multi-page navigation!


### Semantic elements
Before HTML5, a group of HTML elements could be wrapped in `<div>` with an `id` or a `class` which was targeted to style that content. This can lead to confusion on a page because it can be difficult to tell which element does what. **Semantic elements**, introduced in HTML5, are used to define the role some content plays on a website. They don't have default styling and exist to help developers and browsers understand the code better.

`header` : Defines the header of a page or a section. It often contains the title of a page, and a tagline/subtitle.

```html
<header>
  <h1>Page Title!</h1>
</header>
```

`footer` : Defines the footer of a page or a section. It can sometimes contain information about the page, such as who wrote/developed it, copyright information and sometimes links to related files/documents.

```html
<footer>
  <p>Copyright 2014</p>
</footer>
```

`main` : Used for the main content of your page. It should only be used once within your document.

```html
<main class="content">
  <p>Here's some content</p>
</main>
```

`nav`: Defines a section that contains links to other parts of your website. Pssttt... You can have more than one `nav` on your web page. 

```html
<nav>
  <ul>
    <li><a href="home.html">Home</a></li>
    <li><a href="page.html">Page</a></li>
  </ul>
</nav>
```

`section`: Defines a section in a document. The elements nested inside of a `section` often share a similar theme. 

```html
<section class="about">
  <h2>About our class</h2>
  <p>Our class is composed of many different people.</p>
  <p>We're humans learning to code.</p>
</section>
<section class="skills">
  <h2>Skills</2>
  <p>We know HTML, CSS, JavaScript and Fun</p>
</section>
```

`article` : Defines a complete and independent piece of content on your site. For example, it's typically used for a post in a blog, a news article or individual comment.

```html
<article>
  <p>Vestibulum id ligula porta felis euismod semper. Donec sed odio dui.</p>
</article>
```

`aside`: Defines a section of content that is secondary to the main content. Often used as a sidebar.

```html
<aside>
  <p>Vestibulum id ligula porta felis euismod semper. Donec sed odio dui.</p>
</aside>
```

`figure`: Specifies an image, code chunk, illustration, or a diagram. Sometimes it may have `img`, `code` or `video` and `figcaption` elements nested inside of it. Figures are also self containing. Ideally, figures can be moved to a different part of the page without affecting the flow of content.

```html
<figure>
  <img src="images/mysweetpicture.jpg">
</figure>
```

`figcaption`: Defines a caption for the figure item. There should only be one figcaption nested inside of a figure (not all figures need a figcaption). Figcaption can be included before or after the contained element.
```html
<figure>
  <figcaption>A graph of Donald Duck's transformation into Tony Hawk</figcaption>
  <img src="images/mysweetpicture.jpg" alt="A cartoon duck on a skateboard ollie-ing over a canyon, that is also a graph." >
</figure>
```

That's a lot of semantic elements to remember! 😳

It's okay, we don't expect anyone to memorize all of it by the end of this lesson. You can always refer back here. These resources may be handy as well:  
* <a href="https://www.w3.org/TR/html52/" target="_blank">World Wide Web Consortium</a>
* <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element" target="_blank">Mozilla Developer Network</a>

> **Accessibility tip**
>
> Check out `<abbr>`, `<time>`, `<address>`, and `<cite>` as these are often overlooked semantic elements you may find have use in a lot of the code you'll be writing. Remember, user experience with assistive technology will be greatly improved. 

### Exercise
Let's	download and open up [fixThisMarkup.zip](https://hychalknotes.s3.amazonaws.com/fix-this-markup-bootcamp.zip) to practice semantic HTML markup and best practices for HTML.
