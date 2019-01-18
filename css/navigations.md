# Navigations

Almost all navigations on the web are unordered lists filled with list items and links. Let's start with a really simple example. Open up <a href="https://hychalknotes.s3.amazonaws.com/simple-nav.html" download>simple-nav.html</a> in your browser and editor and we will work through an example.

First off we need to take the default margin and padding off that unordered list:

```css
ul {
  margin: 0;
  padding: 0;
}
```

Now we need them to be displayed beside each other, instead of breaking onto the next line. How would we do that?

Remember `display: inline-block;` ? By using this on the list items, they will jump up beside each other.

```css
ul li {
  display: inline-block;
}
```

Note how the bullets disappear by default. We have a problem though - because `inline` elements (including `inline-block`) are whitespace-dependent, we now have some extra layout issues to deal with.

However, we don't want our markup to affect our styles, so instead of `display: inline-block;` we can float the list items left and set the list-style-type to none to remove the bullets.

```css
ul li {
  /*display: inline-block;*/
  float: left;
  list-style-type: none;
}
```

We can now go ahead and style it as we wish.

Note: it is best practice to put your styles on the link themselves rather than the `<li>` because we want the entire link to take up all the space.

## Accessibility and navigations
Allowing users the ability to get to the main content for your site is important. The main content is probably not the first thing on your site, an important piece to creating an accessible site is creating a link to skip to the main content. The idea is fairly straightforward, the first bit of content on the pages is an anchor tag that links to an id further down. <a href="https://www.canada.ca/en.html" target="_blank">See an example of a skip link in action on the Government of Canada's site.</a>

```html
<body>
  <a href="#maincontent" class="skip-link">Skip to main content.</a>

  <!--- Much further down --->

  <main id="maincontent">....</main>
</body>
```

```css
.skip-link {
  position: absolute;
  left: -1000px;
  top: 5px;
  z-index: 999;
  background: white;
  color: black;
}

.skip-link:focus {
  left: 0;
}
```

You also want to use CSS to hide the anchor until the user uses they keys to focus on the anchor. For more information checkout this <a href="http://webaim.org/techniques/skipnav/" target="_blank">link</a> for more information

## Dropdown navigations

A really useful part of doing navigations with unordered lists is that we can create dropdown navigations with nothing but a few CSS rules, some clever positioning and the `:hover` state.

Let's work through an example. Things can get a little confusing here so stay with me. Open up <a href="https://hychalknotes.s3.amazonaws.com/dropdown-nav.html" download>dropdown-nav.html</a> and you'll see a basic navigation unordered list.

Let's style the list and nested list different colours so we know what's going on. While we're at it, change the color of the anchor tags to black:

```css
.main-menu {
  background: yellow;
}

ul.sub-menu {
  background: #ececa9;
}

.main-menu li a {
  color: black;
}
```

Now we need to make the first list items next to each other:

```css
.main-menu li {
  float: left;
  list-style: none;
}
```

Hrm, but that makes both the parent nav and the sub nav inline, we only want the parent nav to be inline, so let's revert the second nav:

```css
ul.sub-menu li {
  float: none; /* Set the sub navs list items back by removing the float */
}
```

The above uses parent &rarr; child selectors to select only those list items nested inside another unordered list.

Okay, looking okay so far. Let's get the hover part working. The first thing we need to do is hide the submenus by default.

```css
ul.sub-menu {
  background: #ececa9;
  display: none;
}
```

Then, how do we show them only when we hover? What should we trigger the hover on?

Since the sub nav is nested inside of the parents `<li>`, we want to trigger it on there. We use `display: block;` to switch it back from `display: none;`

```css
.main-menu li:hover ul {
  display: block;
}
```

Now you should see the sub nav when you hover over its parent:

Problem now is that it pushes everything after the sub navigation down? Why? Because we are using `display: block;` !

If only we could position it that it did not take up any extra space. It should "give up its seat". This is where we start to use `position: relative` and `position: absolute;`

We want the sub menu to be absolute so it doesn't take up any room within its parent and the parent `<li>` to be relative so we can base out positioning off of that.

```css
.main-menu li {
  float: left;
  list-style: none;
  position: relative;
}

ul.sub-menu {
  background: #ececa9;
  display: none;
  position: absolute;
}
```

Bam! with just that, we now have a very simple dropdown menu. It works! We can use CSS to make cosmetic changes in the future.

Did this on your own? <a href="https://hychalknotes.s3.amazonaws.com/dropdown-navANSWER.html" download>Check your answer here!</a>

## Using lists and positioning together

Another great use of lists and positioning are to make galleries with text that appears on hover.

Open up <a href="https://hychalknotes.s3.amazonaws.com/gallery-grid.html" download>gallery-grid.html</a> and use your creativity to code a gallery. You can tackle this in partners if you wish.

This is the <a href="https://hychalknotes.s3.amazonaws.com/gallery-gridANSWER.html" download>answer.</a>