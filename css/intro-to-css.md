# Intro to CSS
HTML is used to describe our content and give our pages structure. We need to use a different language to control how our pages look.

We use _cascading stylesheets_ (CSS) to style our pages. CSS is a stylesheet language that applies styles to various elements on our page. You can control the look, feel, size, colour and virtually any visual aspect of the HTML elements on your page. 

## CSS rule breakdown
Developers can control the style of HTML elements using _rules_. Here is a rule that will change text color of all  `h3` elements on the page to red:

```css
 h3 {
   color: red;
 }
 ```
The _selector_ chooses the elements to which the styles will apply. In the example above, `h3` is the selector. There are lots of ways to make selectors more complex, and we'll explore those later. For now, just know that a selector targets the element to which the styles will apply.

The _declaration_ is everything inside the curly braces, where we define our styles. Inside the curly braces, we include a _property_ and _value_. In the example above, the property is `color` and the value is `red`.

![Diagram](https://hychalknotes.s3.amazonaws.com/diagrams.png)

We can include as many properties and values as we want for any selector, just remember to use a colon in between the property and value as well as end each declaration with a semicolon.

```css
h3 {
  font-size: 16px;
  background-color: yellow;
  color: red;
  /*etc...*/
}
```

### Colors in CSS
In the coming classes, we take a look at all the different ways to choose a color as a value, but we'll look at two right away:

* **color keyword**: You can use the name of the colour - for most basic colours (red, green, blue, pink...) as well as a few exotic ones like `papayawhip` and `palegoldenrod`.
```css
h3 { 
  color: palegoldenrod;
}
```
* **hex value**: You can use a hexadecimal code, which is written with a number sign `#` and a 6-digit alphanumeric code. 

```css
h3 { 
  color: #992283;
}
```

## Where to write your CSS
There are three ways to include CSS in your HTML document.

* **External stylesheet** : This is by far the most common method of including CSS. You create a new file in your project folder and name it whatever you want followed with a file extension of `.css`. It's common for this document to be named `style.css`, `global.css`, or `main.css`. We then write all of our CSS inside of this file and use a `<link rel="stylesheet" href="">` tag in our HTML page's `<head>`.

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Document</title>
    <link rel="stylesheet" href="styles/main.css">
  </head>
  <body>

  </body>
  </html>
  ```

This linking method is most common because most sites have multiple pages that need the same styles. Linking a single stylesheet means that style changes made in a single file will be reflected on the entire site.

* **Internal stylesheet**: Inside your HTML file, you can create a `<style></style>` tag and write your CSS inside.

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Document</title>
    <link rel="stylesheet" href="styles/main.css">
    <style type="text/css">
      h2 {
        color:red;
        font-size:50px;
      }
    </style>
  </head>
  <body>

  </body>
  </html>
  ```
The `<style>` tag tells the browser that you are no longer writing HTML and everything inside of the tags is CSS. Though it will work when placed anywhere on the page, it's convention to include it in the `<head>` element of your document.

This is a method we will use often in class exercises because it allows us to write our CSS and HTML in the same file. 

* **Inline styles**: You can style elements directly in the HTML using the `style` attribute. 

  ```html
  <h2 style="color:red; font-size:50px;">Hello, I'm a header with inline styles</h2>
  ```

The downside to this is that those styles only apply to that specific instance of that element. Not very efficient! Also, these styles supersede the styles from your CSS file, which can cause conflict and confusion.

## CSS playground
Writing CSS from scratch can be confusing if you are new to the game. The best way is to take some existing CSS, read it over, understand it, and hack it. Break things! Anything can be undone or fixed; it's easy to be nervous when you're playing with something new, but one of the best ways to get comfortable with code is to remember that you can experiment and make mistakes with no consequences.

<!-- Go ahead and open up [css-fun.html](https://hychalknotes.s3.amazonaws.com/3.1-css-fun-bootcamp.zip) in both your browser and your text editor. Change the CSS values and see what happens!

### Adding your own markup
To get a handle on how to add and style your own markup, create an additional section with a class of `testimonials` right after the description section in [css-fun.html](https://hychalknotes.s3.amazonaws.com/3.1-css-fun-bootcamp.zip). Add a few additional paragraphs and images to this new section. You can use the absolute path to an image online or include an image in your folder locally and link to the relative path. Add an `h3` heading above the text and inset the image (allow the text to wrap around it like it does on the image in the description section). You should use the proper HTML tags to insert the content. Good luck and be sure to ask questions as you go along. -->