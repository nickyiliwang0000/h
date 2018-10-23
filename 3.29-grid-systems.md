## Grid System

Within graphic design circles, a grid system is used to structure content and create organize elements on a page.  It is used to create columns that span the page at different widths, and maintain equal margins between.

Within web design, it can be used to help layout designs and build your structure quickly, as well as provide an easy route for making your site responsive.

### What does it look like?

#### Bricks
The best way to visualize a grid system is to think of bricks. Some bricks may be longer than others, but together they create a horizontal row that is 100%. The next row of bricks is on top of that row, creating a structure. In between the bricks is an equal amount of cement that gives it spacing and it's distinctive look.

![brick wall](http://i.imgur.com/qnoiBnUl.jpg)

#### Newspaper
Another example is a newspaper. There is equal distance between each paragraph, headline and section.

![newspaper](http://i.imgur.com/nWvJRrD.jpg)

#### Web Design Grid System

![12 Column Grid System](http://i.imgur.com/f2IfouCl.png)

#### Terminology

As you work with Grid systems, you'll come across certain terminology. In an effort to make working with a grid clearer, here's some key terms.

**Fixed**
A definite width of each column. Not flexible.

**Fluid**
A relative width of each column, Flexible and responsive. Typically used with a container div that has a max-width.

**Column**
A vertical width that represents a section of content. Grid systems often use 12 or 16 columns. These exist within a row. Each row must contain a complete set of columns. (eg 1 row = 12 columns)

**Row**
A 100% width that spans horizontally across the page. A row is made up of a complete set of columns.

**Gutter**
The distance between each column. Allows equal margin between elements.

**Presentational**
The use of classes on elements to define width. The layout is defined within the HTML using classes in CSS.
```html
	<header class="col-12"></header>
```
**Non-Presentational**
The use of css to define classes, leaving us with clean HTML markup. Best used with Sass, LESS and Stylus.
```html
	<header></header>

	header {
		@include column(12);
	}
```
### Understand layout with a Grid system

In order to use a grid system, we visualize the number of columns we want an element to take up, and provide that information, instead of a setting. Take the example below

![grid example](http://i.imgur.com/ZUPVIk7l.png)

The site above consists of a header and footer that are both 100% width, then a section that floats next to an aside. To do this without a grid, we'd have to use floats that would need to be cleared and set a margin between the elements. Using a grid system, we can simply state how many columns each section should take up.

**Header** = 12 Columns

**Section** = 7 Columns

**Aside** = 5 Columns

**(Section + Aside)** = 12 Columns

**Footer** = 12 Columns

### Grid systems

There are many grid systems out there, and which one is the best for your project is up to you. There are many factors you need to account for including, fluid vs fixed, # of columns, presentational vs non-presentational.

Here is a collection of the most common used Grid systems.

* Bootstrap - [http://getbootstrap.com/css/#grid](http://getbootstrap.com/css/#grid) (Fluid, Presentational, 12 Column)
* Zurb Foundation - [http://foundation.zurb.com/docs/components/grid.html](http://foundation.zurb.com/docs/components/grid.html) (Fluid, Presentational, 12 Column)
* Bourbon Neat - [http://neat.bourbon.io/](http://neat.bourbon.io/) (Fluid, Non-Presentational, 12 Column)
* Semantic GS - [https://github.com/tylertate/semantic.gs](https://github.com/tylertate/semantic.gs) (Fluid, Non-Presentational, 12 Column)
* 960 Grid - [http://960.gs/](http://960.gs/) (Fixed, Presentational, 12 Column)
* Profound Grid - [http://www.profoundgrid.com/](http://www.profoundgrid.com/) (Fluid, Non-Presentational, 12 Column)
* Responsive Grid System - [http://www.responsivegridsystem.com/](http://www.responsivegridsystem.com/) (Fluid, Presentational, 12 Column)

With all of these grid systems, you will need to download or link the needed CSS files. 

### Bootstrap and Foundation

Within the development world, CSS frameworks exist to help members of the community prototype and design quickly. Two of the most popular frameworks that exist are [Bootstrap](http://getbootstrap.com/) and [Foundation](http://foundation.zurb.com/).

While HackerYou doesn't go into detail with these framework grids, it's important to note that you **already know how to use them**. The frameworks are a collection of pre-written CSS that you apply through the use of HTML and classes. 