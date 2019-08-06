# Navigations

Almost all navigations on the web are unordered lists filled with list items and links. Let's start with a really simple example. Open up [simple-nav.html](https://hychalknotes.s3.amazonaws.com/simple-nav.html) in your browser and editor and we will work through an example.

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

Since we're using floats, we also have to remember to add in a clearfix snippet at the top of our CSS, and to give the `ul` a class of `clearfix` in our HTML.

```css
.clearfix:after {visibility: hidden; display: block; font-size: 0; content:''; clear: both; height: 0; }
```

```html
<ul class="clearfix">
  <li><a href="home.html">Home</a></li>
  <li><a href="about.html">About</a></li>
  <li><a href="work.html">Work</a></li>
  <li><a href="contact.html">Contact</a></li>
</ul>
```

We can now go ahead and style it as we wish.

Note: it is best practice to put your styles on the link themselves rather than the `<li>` because we want the entire link to take up all the space.

## Accessibility and navigations
Allowing users the ability to get to the main content for your site is important. The main content is probably not the first thing on your site, an important piece to creating an accessible site is creating a link to skip to the main content. The idea is fairly straightforward, the first bit of content on the pages is an anchor tag that links to an id further down. [See an example of a skip link in action on the Government of Canada's site.](https://www.canada.ca/en.html)

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

You also want to use CSS to hide the anchor until the user uses they keys to focus on the anchor. Check out this [link](http://webaim.org/techniques/skipnav/) for more information

### Mobile navigations

When building out your navigation menu to contain a mobile hamburger menu, we recommend the following HTML structure:

```html
<header>
  <nav >
    <button>MENU Toggle</button>
    <ul>
      <li>Menu Item 1</li>
      <li>Menu Item 2</li>
      <li>Menu Item 3</li>
    </ul>
  </nav>
</header>
```

It's important to use native semantic elements when possible. Using `nav` here will inform assistive technologies of the presence of a navigation menu. Additionally, by making the `button` element a child of the `nav`, assistive technologies will associate it's relevance to the navigation when reading the menu content to a user.

> **Accessibility tip**
>
> When possible, avoid hiding the `<nav>` element because it provides semantic meaning to assistive-technology. When scanning a website, devices like a screen-reader will inform users that there is a collection of list items that are intended for page navigation. When this element is hidden, that information will not be shared. If you need to hide nav items (to show/hide on click, for example), try to only hide the embedded list elements, leaving the nav element on the page to be visible to screen readers. 


## Dropdown navigations

A really useful part of doing navigations with unordered lists is that we can create dropdown navigations with nothing but a few CSS rules, some clever positioning and the `:hover` state.

Let's work through an example. Open up [dropdown-nav.html](https://hychalknotes.s3.amazonaws.com/dropdown-nav.html) in your editor and browser. We'll be working towards [this](https://hychalknotes.s3.amazonaws.com/dropdown-nav-ANSWER.html).

Let's style the list and nested list different colours so we know what's going on. While we're at it, change the color of the anchor tags to black:

```css
.main-menu {
  background: yellow;
}

.sub-menu {
  background: #ececa9;
}

.main-menu li a {
  color: black;
}
```

Now we need to make the first list items sit next to each other:

```css
.main-menu li {
  float: left;
  list-style: none;
}
```

Again, we're using floats, so don't forget to define a `clearfix` class at the top of your CSS and to add it to the `.main-menu` in your HTML.

The problem with what we've done is that it makes both the parent nav and the sub nav inline. We only want the parent nav to be inline, so let's revert the second nav:

```css
.sub-menu li {
  float: none; /* Set the sub nav's list items back by removing the float */
}
```

Okay, looking okay so far. Let's get the hover part working. The first thing we need to do is hide the submenus by default.

```css
.sub-menu {
  background: #ececa9;
  display: none;
}
```

How do we show them only when we hover? What element should we trigger the hover on?

Since the sub navs are nested inside of parent `<li>` elements, we want to make the sub navs visible when the user hovers on their respective parent list items. We use `display: block;` to switch it back from `display: none;`

```css
.main-menu li:hover ul {
  display: block;
}
```

Now you should see the sub nav when you hover over its parent. However, the problem now is that it pushes everything after the sub navigation down. Instead, we want it to be positioned on the page such that it doesn't take up any room within its parent or shift other elements around. We can accomplish this by giving the sub nav `position: absolute;` and the parent `li` `position: relative;`:

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

We now have a very simple dropdown menu, and we can use CSS to make cosmetic changes in the future.

## Using lists and positioning together

Another great use of lists and positioning are to make galleries with text which appears on hover.

Open up [gallery-grid.html](https://hychalknotes.s3.amazonaws.com/gallery-grid.html) and use your creativity to code a gallery. You can tackle this in partners if you wish.

This is the [answer](https://hychalknotes.s3.amazonaws.com/gallery-gridANSWER.html).
