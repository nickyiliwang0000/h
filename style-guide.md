# Style guide

## Conventions
* Each tab is 2 spaces and tabs are converted to spaces before uploading files.
* Include the filename in the code snippet for code-alongs
```html
  <!-- index.html -->
<section>
  <p>some text</p>
  <p>some text</p>
  <p>some text</p>
  <p>some text</p>
</section>
```
  unless the example is wholly self-contained:

  ```javascript
  class Button extends Component {
    render() {
      return (
        <button onClick={this.handleClick}>Add to cart</button>
      )
    }
  }
  ```
* Include student takeaway at the beginning of every lesson
  ```markdown
  <!-- Student takeaway -->
  <!-- By the end of this lesson, the student should know:
  - What `controls` & `autoplay` do to the video element 
  - How to provide different sources to a `video` or `audio` element
  - Where to find information about playing video on mobile
  - Where to find information about `video` and `audio`accessibility
  -->
  ```
* use e.g. for examples, use i.e. for a different explanation of the same thing

### Words and phrases
* **web page** NOT webpage
* **website** NOT web site (weird to have these be opposite but these are the most common spellings for each ¯\'_(ツ)_/¯)
* **JavaScript** NOT Java Script or Javascript
* **code-along** NOT codealong or code along (like sing-along)
* **pseudo-element** NOT pseudoelement or pseudo element
* **pseudo-class** NOT pseudo selector or pseudo-selector
* **internet** NOT Internet

#### Markdown-specific conventions
* new words like _this_
* important phrases/words like **this**
* backticks to denote code or typing instructions `div`, `cmd + V`
* single quotes to denote menu options or through a program directions
* Unordered lists with `*`, not `-`

##### Examples:
```markdown
The word _enchiridion_ means "handbook".
**This is the most important thing to remember**
 `div` or `cmd + V`
 Go to 'File' > 'Open Recent' 
```
##### Example file structure layout
```bash
- projectOne
  index.html
  - styles 
    - partials
      style.scss
      style.css
  - images
      logo.png
      background-image.jpg
```
Folders have - in front of them
contents of a folder are indented
files and folders on the same level 

## Example lesson layout
```markdown
# Lesson title in sentence case - mostly lowercase unless you're using a name like HTML or React Router
## Large lesson section  (e.g. HTML elements)
### Lesson subheading (e.g. The span tag)
#### Section subheading (e.g. When to use a span tag)
```

**Incorrect 👎**
```html
<!-- Code example -->
```

**Correct 👍**
```html
<!-- Code example -->
```
