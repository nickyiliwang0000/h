<!-- Student takeaway: -->
<!--Student will be able to:
- Identify clean code
- Know two ways to keep HTML clean (indentation + semantic elements)
- Know three ways to keep CSS clean (indentation + appropriate selectors + DRY)
- Know when to use floats or flexbox (variable content + page layout)
- Know when to use positioning (immutable content + styling tweaks)
- Know to compress their CSS and images
 -->

# Philosophy of best practices for HTML and CSS

_Best practices_ is a nebulous term that sometimes alludes to the web development community's current favorite things. You will never nail down everything that can fall under the umbrella term "best practices" and different people use it different ways. At Juno, best practices are how we encourage ourselves to write clean code. The following is a non-exhaustive list of ways to do that.

As your projects go on, we move some of the previous project requirements into a "best practices" catch-all that you can find [here](https://github.com/HackerYou/bootcamp-notes/blob/master/stuff-you-need-to-know/resources-and-cheat-sheets/best-practices-by-project.md).

## What do we mean by clean code?

Clean code is easy for humans to read. 
Clean code is not repetitive. 
Clean code is organized according to a system that a reader can repeat. 
Clean code is rewritten as you go, not left for someone else to fix later. 
Clean code has clear boundaries. 
Clean code doesn't have a bunch of StackOverflow answers smashed in one after another. 
Clean code is you knowing what you want to say and saying it in the most readable, concise way you know how.

So, how do we write clean code?

## We organize our projects
If no one can find our files, no one can see our beautiful, shiny code. As our website projects get bigger, it will become more important to have an system by which to organize them.

### Folder structure
In our first examples, we wrote CSS inside `<style>` tags. This is okay for example or exercises, but the best practice is to separate styles out into their own `style.css` file. Down the road you may have 3 or 4 CSS files that you are working with.

When you have more than one file of any given type, group them into a folder. A nice clean web project that has HTML, CSS, JavaScript, and images would look like this:

```bash
- 2020-coca-cola-microsite
    index.html
  - styles
      style.css
      normalize.css
  - js
      script.js
      jquery.js
      plugin.js
  - images
      header-image.jpeg
      logo.png
```
Check out the [keeping organized as a developer](https://github.com/HackerYou/pre-bootcamp-review/blob/master/html/keeping-organized-as-a-developer.md) lesson for more about at organization.

### No spaces!
As developers, we will no longer be creating folder or file names with spaces in them! Computers can't read spaces and they lead to confusing and avoidable issues as our projects get more complex! So get in the habit now of omitting spaces from your folder and files name!

In order to make our file or folder names readable without spaces, we will follow one of the following naming conventions:

- *Camel case*: spaces are removed and the first letter of each word is capitalized.
- *Kebab case*: spaces are replaced with dashes
- *Underscore case*: space are replaced with underscores

It is important to pick one naming convention and stick with it.

## Exercise: Make a well-named folder now!
During your time at Juno, you will be given many exercises and will create many projects.

Within your `sites` or `websites` folder, create a new folder called `juno`. Within that new folder, create a folder for each week of the bootcamp.

```bash
- websites 
# (or sites)
  - juno
    - week1
    - week2
    - week3
    - week4
    - week5
    - week6
    - week7
    - week8
    - week9
```

When working on a project, open the entire project folder in your text editor. This should help you stay clear on which file belongs to which project.


## We keep our HTML files readable
### HTML indentation
As your write longer and longer HTML documents, you're more likely to get lost. We already learned that code comments can help show you where you are in your code, but even more important is **keeping your elements properly indented**.

Which piece of code is easier to read?

```html
<!DOCTYPE HTML>
<html lang="en-US">
<head>
<title>CSS Exercise</title>
</head>
<body><div class="wrapper">
<header>
<h1>My Website</h1><nav></nav>
</header>
<main class="content">
<!-- Page content goes here -->
</main>
<footer>Copyright Hacker You 2018
</footer></div><!-- /.wrapper -->
</body>
</html>
```

OR

```html
<!DOCTYPE HTML>
<html lang="en-US">
  <head>
    <title>CSS Exercise</title>
  </head>
  <body>
    <div class="wrapper">
      <header>
        <h1>My Website</h1>
        <nav></nav>
      </header>
      <main class="content">
        <!-- Page content goes here -->
      </main>
      <footer>
        Copyright Hacker You 2018
      </footer>
    </div><!-- /.wrapper -->
  </body>
</html>
```

The second one is longer, but you are able to get an idea of the page structure almost right away. If you are messy with indentation, chances are you end up spending 15 minutes searching for a `div` tag that is not closed properly.

Indenting code is easy: press the `tab` button in front of your line. Most good text editors will automatically indent your code as you write it as well as providing shortcuts for indenting large blocks of code.

<!-- * Sublime Text 3
  Sublime Text has a shortcut for **paste and indent**:

  Instead of pressing `cmd/ctrl + v` to paste, press `cmd/ctrl + shift + v` to paste and indent properly.

  Sometimes you will also have to indent several lines at a time. To do this, select all the lines you want and press `cmd/ctrl + }` to indent all of them at once, forward and `cmd/ctrl + {` to indent back. -->

* VSCode
  VSCode has a setting for paste and indent:

  Go to your user settings in VSCode and add `"editor.formatOnPaste": true` or search for `format` and check the `formatOnPaste` box.
  ![screenshot of VSCode formatOnPaste screen](https://hychalknotes.s3.amazonaws.com/vscode-format-on-paste-screen.png)

### Semantic elements: `div` vs. list

We harp a lot on semantic elements for good reason. HTML is used to describe the meaning of the content to the browser.  There are many obvious cases where a semantic element like `header`, `footer`, or `article` makes more sense than `div`. But what about when you've got:
* a gallery of images?
* a roll of blog posts?
* a set of social icons?

They could be contained within a `div`, but a more semantically accurate element to contain them might be a list. 😦 😯 🐡 **Mind = blown.** 😦 😯 🐡

## We keep our CSS files readable
### CSS indentation 
It is best practice to have the selector and opening bracket, each rule, and the closing bracket on separate lines.

**👎 Not so good**
```css
h2 {    color:red;
font-size:50px; }
```

**👍 Best**
```css
h2 {
  color:red;
  font-size:50px;
}
```

When there is only one rule for a selector, it's acceptable to put the entire declaration on a single line.

```css
h2 { color:red; }
```
### CSS organization
CSS can become a tangled mess if isn't managed properly. You might have multiple selectors styling the same element, or a rule that doesn't apply because the style is being re-defined somewhere else. It can be a real headache.

Some tips to help you manage CSS files:
* Add comments to your CSS!
* Order your CSS ([by type](http://css-tricks.com/poll-results-how-do-you-order-your-css-properties/)) to help you stay organized. 
* Only be as specific in your selector as you need to be.
* Use advanced selectors where appropriate. [Bookmark this cheatsheet!](http://code.tutsplus.com/tutorials/the-30-css-selectors-you-must-memorize--net-16048)
* Avoid using toooo many selectors.
  CSS selectors are read from right to left by the browsers. For example, to read the selector `body #container ul li`, the browser will evaluate `li` then `ul li` then `#container ul li` and the full selector. If you have just one unordered list on your page, `li` is sufficient to apply the right style.
* Use classes to replace very nested selectors.
  If you've got, say, a bunch of list items that are social icons, choose to make a class `.social-icons-list` for their parent `ul` (or target `ul` if there's only one), instead of targeting `body footer section div.contact-us ul`.
* Remember that IDs are by definition unique so instead of `div#container` you only need `#container`.

## We don't repeat ourselves

If you have two (or more) elements that are mostly styled the same, avoid writing the same CSS rules twice. Write one set of rules for their shared properties and then add individual rules as needed.

**👎 Not so good**
```css
.box1 {    
  width: 300px;
  height: 50px;
  padding: 10px;
  color:#f8a;
}
.box2 {    
  width: 300px;
  height: 50px;
  padding: 10px;
  color:#444;
}
```

**👍 Better**
```css
.box1, .box2 {
  width: 300px;
  height: 50px;
  padding: 10px;
}
.box1 {
  color: #f8a;
}
.box2 {
  color: #444;
}
```

An even better way is to create a class that you can reuse for both boxes:

**👍 Best**
```css
.box {
  width: 300px;
  height: 50px;
  padding: 10px;
}
.box1 {
  color: #f8a;
}
.box2 {
  color: #444;
}
```

Developers in many languages have taken up the _don't repeat yourself_ (DRY) mantra; it'll become a buzzword again when we move into JavaScript.

## We use the correct tools for the job when creating page layouts

### Floats or flexbox vs position

If floats, flexbox, and `position` can all be used to align elements, how do we know when to use each one?

**Recommended usage for floats and/or flexbox:**
* Containers for content whose size you can't predict
  * because the content is dynamic (e.g. loaded from an API)
  * because user action will change it (e.g. resizing the browser)
* Laying out block elements related to the structure of the page.

**Recommended usage for positioning:**
* Placing content that doesn't interact with the flow of the page (e.g. a fixed navigation).
* Orienting elements within a specific block of the page (e.g. a badge or banner on a list item for sale).
  * Note: When you change an element's `position` to `absolute` or `fixed`, any floats applied to that element no longer apply.

> Grid systems are used for layout, sometimes in concert with flexbox or floats. Think of them as members of the first group.

### Margin and padding

Padding adds space **inside** an element. It does not accept negative values.

Margin adds space **outside** of the element. Margin accepts negative values, which can have the appearance of **removing** space from outside the element and thereby forcing elements to overlap.

**Recommended usage for margin and padding:**
* To style spacing within and around the element, **not** for page layout or positioning large structural blocks.

## We compress our files

Compressing (or _minifiying_) CSS and image files will make our sites faster. Compressed CSS has unnecessary whitespace and characters removed to reduce the size of the file. 

Lossless image compression will optimize images by removing unnecessary bytes without affecting image quality. 

(Read more about image compression [the lesson on image formats](https://github.com/HackerYou/bootcamp-notes/blob/master/css/image-formats-and-svg.md).)

* [csscompressor.com](http://www.csscompressor.com/), a CSS minification tool
* [imgopt.com](http://www.imgopt.com/), an image compression tool
* [kraken.io](https://www.kraken.io/), an image compression tool
* [imageoptim.com](http://imageoptim.com), an OSX image compression tool

In addition to compressing your images, it's always a good idea to crop them to an appropriate dimension before using them on the web. Users shouldn't have to download a 2000px hi-res photo if it's only going to be 200px wide on their screen.
