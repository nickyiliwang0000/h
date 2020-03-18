<!-- Student takeaway: -->
<!--Student will be able to:
- Name 3 preprocessors (Sass, Less, Stylus)
- Write an SCSS variable
- Nest selectors in SCSS
- Properly link images from .scss files
- Write an SCSS mixin
- Write and properly link a SCSS partial
- Be aware of SCSS functions
-->

# CSS preprocessors
CSS preprocessors are bundles of code that you can install in your projects to automate some of the frustrating or repetitive tasks writing good CSS requires. The most popular CSS preprocessors are:

* [Sass](http://sass-lang.com/) (Syntactically Awesome Style Sheets) 
* [Less](http://lesscss.org/) (Leaner Style Sheets)
* [Stylus](http://stylus-lang.com/) (expressive, dynamic, robust CSS)

But why should I change my CSS workflow? Why make CSS more complicated? Because CSS preprocessors extend the basic functionality and overcome many limitations of traditional CSS by adding features such as variables, nesting, and mixins. These features will help you write CSS that is more maintainable, organized, and modular.

While each preprocessor language follows similar rules, each has its own syntax (different from traditional CSS) and must be saved with an associated file extension.

Preprocessor | File extension
--- | ---
Sass | `.scss` or `.sass`
Less | `.less`
Stylus | `.styl`

Because browsers can only read CSS files with the `.css` extension, preprocessor files need to be _compiled_ into regular CSS files before they can be used on the web. 

![diagram of css compiling flow](http://cl.ly/image/1W0E2w1l1j3q/compiling-scss.png)

## Sass (Syntactically Awesome Style Sheets)

Let's explore the power of preprocessors using Sass. Remember that sass is an extension of CSS, so all regular CSS is also valid Sass! Use as much or as little Sass as you're comfortable with when you're getting started.

![diagram showing Sass as a superset of CSS](http://cl.ly/image/15293X1N0c0J/sass-css.png)

The workflow Sass is that you will write your styles in `style.scss`and then compile it into a `style.css` file. The CSS file is the one you want to link to in your HTML. **If you link to your SCSS file, the styles will not load.**

There are a variety of applications available to compile our `.scss` or `.sass` files to `.css`. We are going to use a Visual Studio extension called [Live Sass Compiler](https://marketplace.visualstudio.com/items?itemName=ritwickdey.live-sass). 

Alternatively, [Prepros](https://prepros.io/) is a widely used free option.

To get a project setup with Live Sass Compiler, we can use this [guide](https://github.com/HackerYou/bootcamp-notes/blob/master/stuff-you-need-to-know/resources-and-cheat-sheets/live-sass-setup.md).

We may also need to install an SCSS package in our text editor. 

### Sass syntax

It's important to know that there are two syntaxes available for Sass. _Sassy CSS_ (SCSS) is what we'll be using in these examples.

The other (older) syntax available is just called (confusingly) SASS and uses the `.sass` extension. SASS syntax has indentation and new lines rather than brackets and semicolons to separate properties. You might find this easier to read and quicker to write - if so, feel free use it. 

```scss
/* This is SCSS syntax */
ul {
  display: flex;
  background: black;
    li {
    flex: 1 0 auto;
      a {
        display: inline-block;
        padding: 10px;
      }
  }
}
```

```scss
/* This is SASS syntax */
ul
  display: flex
  background: black
    li
      flex: 1 0 auto
      a
        display: inline-block
        padding: 10px
```

### SCSS variables

Variables are used to hold values. For example, you can specify a colour value to an easy-to-remember variable name and reuse it throughout the stylesheet.

The variable name is set/declared in one place but can be used wherever the value is needed.

Example:

```scss
$primary: #B3EB95;
$secondary: #CCC;
$baseFont: "HelveticaNeue-Light", "Helvetica Neue Light", "Helvetica Neue", Helvetica, Arial, "Lucida Grande", sans-serif;

a.home {
  background: $primary;
}

p.tagline {
  border: 1px solid $primary;
  color: $secondary;
  font-family: $baseFont;
}
```

Variables lessen the amount of repetition you have in your code. By collecting common styles and assigning them a simple, memorable name, you can cut down production time.

### Nested SCSS

You can nest selectors instead of using long selector names. A nested selector represents a child element. This keeps your stylesheet organized and saves some space. You can even tack on pseudo selectors in a nested rule using the `&` symbol!

This SCSS code
```scss
$primary : #B3EB95;

ul.nav {
  background:red;
  width:100%;
    li {
    border-right:1px solid $primary;
      a {
        background:$primary;
        padding:10px;
        
        &:hover {
          background: yellow;
        }
    }
  }
}
```

Compiles to this CSS:

```css
ul.nav {
  background: red;
  width: 100%;
}

ul.nav li {
  border-right: 1px solid #B3EB95;
}

ul.nav li a {
  background: #B3EB95;
  padding: 10px;
}

ul.nav li a:hover {
  background: yellow;
}
```

**The Sass Inception Rule:** 
> [Never nest more than three levels deep.](<http://thesassway.com/beginner/the-inception-rule>)

### SCSS partials

_Partials_ are what we call small SCSS files that hold styles for a particular part of your page. Navigation styling, button styling, or styling for a page that is different from the rest of your design are all good candidates for partials. You'll stitch them together using your preprocessor when you compile your code. Partials can help keep your styles organized and more maintainable. 

To create a partial, prepend the file name with a `_`. This will tell the compiler to treat it as a partial and not create a separate CSS file for it.

```bash
  _normalize.scss
  _nav.scss
```

To import the partial, use the `@import` keyword, followed by the name of the partial. You do not need to include the underscore or the extension. Sometimes your `styles.scss` file will be mostly imports!

```scss
@import "normalize";
@import "nav";
```

If you have created a separate folder to store the partials, you will have to create the path to the file.

```scss
@import "partials/normalize";
@import "partials/nav";
```

### SCSS functions

Sass has something called functions which can do some of the hard work for you. Let's take a look at a few:

<http://sass-lang.com/documentation/Sass/Script/Functions.html>

A couple that you may find particularly useful are the  [`lighten`](http://sass-lang.com/documentation/Sass/Script/Functions.html#lighten-instance_method) and [`darken`](http://sass-lang.com/documentation/Sass/Script/Functions.html#darken-instance_method) functions. They create a lighter or darker version of any colour. 
 
 ```scss
$primary : #B3EB95

a.home {
  background:$primary;

  &:hover {
    background: lighten($primary, 10) //10% lighter than $primary;
  }

  &:visited {
    background: darken($primary, 10) //10% darker than $primary;
  }
}
```

### SCSS mixins

Mixins are for when we want to repeat similar chunks of code with slight variations. When we declare the mixin, we use the placeholder variable for the value of the CSS property that will change. 

```scss
/*in this mixin declaration, $sizeValue is the placeholder*/
@mixin fontSize($sizeValue) {
  font-size: $sizeValue;
  color: blue;
  font-weight: bold;
}
```
When the mixin is used, we pass in the value we need, and that value replaces the placeholder variable.	

```scss
h1 {
  /* when we use the mixin, we replace the placeholder with the actual value we want */
  @include fontSize(36px);
}

p {
  @include fontSize(14px);
}
```

Compiles to
```css
h1 {
  font-size: 36px;
  color: blue;
  font-weight: bold;
}

p {
  font-size: 14px;
  color: blue;
  font-weight: bold;
}
```

We can even get Sass to do math for us! Say we want it to dymanimcally generate our font sizes in rems with a pixel fallback. So far, we have been setting the base font size in our HTML to 125% to allow for easy rem calculation. Here's how we might make it even easier with a mixin:

```scss
@mixin fontSize($sizeValue) {
  font-size: $sizeValue * 1px;
  font-size: ($sizeValue/10) * 1rem;
}

h1 {
  @include fontSize(48);
}
```

Compiles to

```css
h1 {
  font-size: 48px;
  font-size: 4.8rem;
}
```

Mixins can also accept multiple variables, opening up a whole world of possibilities:

```scss
@mixin position($type, $top, $left) { 
  position: $type; 
  top: $top;
  left: $left; 
}

.box { 
  @include position(absolute, 15px, 30px); 
}
```

When we declare mixins with variables, every variable must have a value passed in when the mixin is being included. However we can make an value optional if we provide a *default value* to the variable when we define the mixin:

```scss
@mixin position($type: relative, $top: 0, $left: 0 ) {
  position: $type; 
  top: $top;
  left: $left; 
}
.box {
  @include position(absolute); 
}
```

Compiles to:

```css
.box {
  position: absolute;
  top: 0;
  left: 0;
}
```
So even if we didn't provide values for `$top` and `$left` variable, SCSS will compile to use the default values provided.

### SCSS gotcha corner
#### How do we link our background images inside of our SCSS files?

You **gotta** link your images using the location of your `.css` file as the base.

If your file structure looks like this:
```bash
- projectOne
    index.html
    - styles 
        style.css
        - partials
            header.scss
    - images
        logo.png
        background-image.jpg
```

Your image path should look like this:
```scss
header{
  background-image:url(../images/background-image.jpg)
}
```

## Let's write some SCSS together!
Let's write some Sass in the folder we dragged into Prepros earlier to see it in action. If you'd like some extra practice, open up [this file](https://hychalknotes.s3.amazonaws.com/getting-sassy--ANSWER.zip) in your browser and write some Sass to recreate it.
