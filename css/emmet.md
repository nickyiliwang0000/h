<!-- Student takeaway -->
<!-- By the end of this lesson, the student should know:
- How to make an element using Emmet
- How to make an element with a class name using Emmet
- How to make an element with an ID name using Emmet
- How to make child elements using Emmet
- How to make multiple elements using Emmet
- How to make sibling elements using Emmet
- How to add attributes to elements using Emmet
- A bunch of CSS tab triggers in Emmet
-->

# Emmet

Now that we're comfortable with the syntax of HTML and CSS, we can leverage some tools to help us write it faster. One of the most popular tools in the industry is [Emmet](http://emmet.io/). Emmet comes pre-installed with Visual Studio Code.

## Emmet and HTML

* `element` + `tab` creates that element and puts your cursor inside:
  * `span` + `tab` → `<span></span>`
  * `div` + `tab` → `<div></div>`
  * `p` + `tab` → `<p></p>`

* `element.className` + `tab` creates that element with the associated class(es)
  * `span.hello` + `tab` → `<span class="hello"></span>`
  * `div.goodDay` + `tab` → `<div class="goodDay"></div>`
  * `p.odd.warning` + `tab` → `<p class="odd warning"></p>`

* `element#idName` + `tab` creates that element with the associated ID
  * `div#contact` + `tab` → `<div id="contact"></div>`

* `element>childElement` + `tab` creates nested elements
  * `ul>li` + `tab` → `<ul><li></li></ul>`
  * `p>span` + `tab` → `<p><span></span></p>`

* `element*5` + `tab` creates that element times the number
  * `span*2` + `tab` → `<span></span><span></span>`
  * `p.hello*2` + `tab` → `<p class="hello"></p><p class="hello"></p>`
  * `div.box.box$*5` + `tab` → `<div class="box box1"></div> <div class="box box2"></div> <div class="box box3"></div> <div class="box box4"></div> <div class="box box5"></div>`

* `element+element` + `tab` creates sibling elements. 
  * `h2+p`+ `tab` → `<h2></h2><p></p>`

If you want to declare an attribute, use `[]`. 
 * `img[src="images/header.png"]` + `tab` →   ` <img src="images/header.png" alt="">`

To add content to the element, use `{}`.
* `h2{Available Courses}` + `tab` →    `<h2>Available Courses</h2>`

Use `()` to group elements together. 
* `article>h2+p*4` is not the same as `article>(h2+p)*4`.

All the above can be mixed and matched. Try some of the following:

* `ul>li.food.food$*10`
* `div.wrapper>div.content+div.sidebar`
* `ul.list.list-number-$*2>li.item.item$*2>h2{intense}+p>span{woah}`

For a little challenge, download and complete this [emmet-exercise.zip](https://hychalknotes.s3.amazonaws.com/emmet-exercise.zip).

## Emmet and CSS

In CSS files, you can usually just type the first few letters of what you want, and Emmet will figure out what you were looking for. Try some of the following:

* `posrel` →  `position: relative;`
* `posab` →  `position: absolute;`
* `fl` →  `float: `
* `fr` →  `float: right;`
* `db` →  `display: block;`
* `dib` →  `display: inline-block;`
* `tdn` →  `text-decoration: none;`
* `c` →  `color: #`
* `w` →  `width: `
* `w100` →  `width: 100px;`
* `w100p` →  `width: 100%;`
* `p` →  `padding: `
* `p10` →  `padding: 10px;`
* `p10p` →  `padding: 10%;`
* `bt` →  `border-top: `
* `bb` →  `border-bottom: `

## Additional resources:

* [Emmet Cheatsheet](http://docs.emmet.io/cheat-sheet/)