# Style guide

## Conventions

* Include the filename in the code snippet for code alongs
 ```html
  <!-- index.html -->
    <section>
      <p>some text</p>
      <p>some text</p>
      <p>some text</p>
      <p>some text</p>
    </section>
  ```
  * unless the example is wholly self-contained:

  ```javascript
  class Button extends Component {
    render() {
      return (
        <button onClick={this.handleClick}>Add to cart</button>
      )
    }
  }
  ```

### 
### Words and phrases
* web page NOT webpage
* website NOT web site (weird to have these be opposite but these are the most common spellings for each ¯\_(ツ)_/¯)
* JavaScript NOT Java Script
* code-along NOT codealong or code along (like sing-along)

#### Markdown-specific conventions
new words like _this_
important phrases/words like **this**

##### example:
**This is the most important thing to remember**
The word _enchiridion_ means "handbook".

# Things to decide
* What do we do for little notes or asides?
* Internet or internet ?

<!-- Example lesson layout -->
# Lesson title (sentence case)
## Heading one (e.g. HTML elements)
### Subheading (e.g. The span tag)
#### Section subheading (e.g. When to use a span tag)