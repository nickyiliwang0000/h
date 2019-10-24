## Before and after elements

We have already learned about pseudo-selectors like `:hover`, `:focus` etc. There are also the similar-looking `::before` and `::after` - these use CSS to create _pseudo-elements_ which appear as the first/last children of the element you apply them to. They can be used to add stylistic/cosmetic touches, like smart quotes, or borders that can be different sizes than the content.

It’s important to note that content inserted into the pages by pseudo-elements is not universally supported by assistive devices and software - some read it, and many do not. For this reason do not use pseudo-elements to insert content that is important to your web page. For any purely stylistic pseudo-elements which can be read aloud, you will need to add additional CSS rules to hide it from the screen readers.

In order to use before/after elements, the `content` CSS property must be supplied. This outlines the content that will be inserted in the pseudo-element; it can be left empty (ie. `content: "";`), but it has to be there.

```html
<span class="name">Cool Person</span>

<style>
   .name::before {
      content : '☃';  
    }
</style>
```

![Snowman icon to the left of Cool Person](https://hychalknotes.s3.amazonaws.com/before-after-cool-person-snowman.png)  

### Notes to keep in mind:

* Pseudo-elements can be added to any element except those which are self-closing, which means they can't be used on images or any kind of input element.
* The syntax officially requires the use of `::`, but many browsers will accept the use of a single colon, ie. `:before` and `:after`.
* Remember, never use pseudo-elements for non-cosmetic page content. CSS should only be used to define style, so if you have something that is part of the actual page content, it should always be in your HTML.

Let's walk through an example. We'll look at two common uses for pseudo-elements - wrapping blockquotes in “smart quotes”, and giving links fancy underlines.

Download the starter file <a href="https://hychalknotes.s3.amazonaws.com/3.15-pseudoElements.html" class="exercise" download>3.15-pseudoElements.html</a> and code along. Open up <a href="https://hychalknotes.s3.amazonaws.com/3.15-pseudoElements-ANSWER.html" class="exercise" download>3.15-pseudoElements-ANSWER.html</a> in the browser to see what we're working towards.

## Making shapes
One of the uses of pseudo-elements is to make decorative shapes. Generally, these shapes do not have any content, but in order for us to create a pseudo-element we will still need to include the content property and provide it with empty quotes as the value.

```html
<span class="name">Cool Person</span>

<style>
.name::before {
  content : '';
  width: 35px;
  height: 35px;
  border-radius: 50%;  
  background: tomato;
}
</style>
```

An important note here is that by default, pseudo-elements are displayed as inline elements. In order for a pseudo-element without content to be visible, it needs to be set to something other than `display: inline`. 

```html
<span class="name">Cool Person</span>

<style>
.name::before {
  content : '';
  width: 35px;
  height: 35px;
  border-radius: 50%;  
  background: tomato;
  display: block;
}
</style>
```

Changing the example above to `display: block` allows the pseudo-element to accept the height and width specified, and therefore be visible.

We can also make more complex shapes using pseudo-elements, shapes which are otherwise impossible in CSS. By using borders with before/after elements, we can create triangles, hexagons, etc.

For a tutorial on how to create these shapes, read <a href="https://medium.com/@jenthorn_/how-to-make-a-hexagon-in-css-8ee61d5ebae5" target="_blank">How to make a Hexagon in CSS</a> by HackerYou alumni, <a href="http://jenthorn.ca" target="_blank">Jen Thorn</a>.

Check out <a href="https://css-tricks.com/animation-css-triangles-work/" target="_blank">this link and find the video that explains how we can use borders to create triangles in CSS!</a>

For more advanced CSS Shapes, <a href="https://css-tricks.com/examples/ShapesOfCSS/" target="_blank">this article on CSS Tricks</a> discusses how to use `:before` and `:after` elements with borders to create some pretty wild shapes. <a href="https://1stwebdesigner.com/css-shapes/" target="_blank">This is also a great resource</a>.

To see how far you can take pseudo-elements checkout <a href="https://a.singlediv.com/" target="_blank">A Single Div</a>