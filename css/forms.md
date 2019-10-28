<!-- Student takeaway: -->
<!--Student will be able to:
- Properly link a label to a form input
- Properly hide a label for a screenreader
- Name 10 types of inputs (there are 16 mentioned)
- Properly use the fieldset element
- Know whether to use a button or an input to submit
-->
# Forms 
Forms are collections of inputs that are used to take in information from a user. When submitted, a form sends that information to a server, which does something with it.

There are four major parts to forms:

* `input`: Input elements accept information from a user. The most common inputs are text boxes that might ask you for something like your email address, password, or username. Other types include checkboxes, ranges, or radio buttons.
* `label`: This element lets users know what each input is for.
* `fieldset` : This element groups parts of a form together.
* `legend`: This is like a label for a group of inputs within a fieldset.
* `form`: This element is how we how we group `fieldset` elements together. All inputs and fieldsets inside of a `form` tag belong to that form and will be sent over the internet when that form is submitted.

Let's take an example from Twitter and break it down:

![Twitter form](http://f.cl.ly/items/3B3u1Y251y1E322q3P0x/Screen%20Shot%202012-10-17%20at%2012.37.19%20PM.png)

We see here two different forms:

1. The sign-in form
1. The register form

They each have different types of inputs because the forms do different things.

* The sign-in form has:
  * an email input
  * a password input
  * a checkbox
  * a submit button

* The register form has:
  * name input
  * an email input
  * a password input
  * a submit button

When the login form is submitted, the browser captures the information in the inputs and sends it information to the servers at Twitter.com. 

## Client-server communication
A _server_ is a big computer somewhere else that hosts a website. A form is an HTML element that renders in a user's browser. The information a user enters is captured when they submit the form.

In our Twitter example, the information from the login form is sent to Twitter's server. Twitter's server then runs some code to decide if the information sent is correct. 

> We won't be touching on any server side languages in this course, but if you do want to explore what happens once you submit the form to the server, you look into learning a language such as Ruby (Ruby on Rails framework), PHP (Code Igniter/WordPress), Python (Django), NodeJS (JavaScript on the server), or ASP /.NET (Microsoft products).

If the information is correct, the server sends a message back to the browser that allows it to display your dashboard. 

If the information is not correct, the server sends back a message that tells the browser to display an error screen.

The important thing to note here is that we use a **form** to send information from the **browser** to the **server**.

Without a connection to a server, forms don't **do** anything. When we work with forms, we are dealing with what are called _server-side technologies_. Our tools (HTML and CSS) are the opposite of this and are termed _client-side technologies_.

Client-side technologies can:
* choose the look and feel of a web app
* display hard-coded information 
* change a button's style when it's focused

Server-side technologies can:
* check if username and password match
* upload a photo
* post a new listing on Craigslist
* add a comment on a blog post
* post a Tweet

Luckily, there are services that do the entire server side part for us. A service like [http://www.focuspocus.io/](http://www.focuspocus.io/) or [https://formspree.io/](https://formspree.io/) will send the data from our forms to a specified email. 
(Note that formspree will only work if your site is live.)

## Input types
Open up [this file](https://hychalknotes.s3.amazonaws.com/inputs.html) and follow along with the input examples. 

Note that most browsers have a bit of form validation built into them. This means that if an input expects a certain form of information (e.g. email, phone number, postal code), the browser will throw an error if the information typed in doesn't match the formatting the input expects (e.g. name@emailprovider.com, 432-232-1214, M3Y 9K8).

### `input[type=text]`
The most common input is a text input:

```html
<input type="text">
```
### `input[type="email"]`

An email input works like a text input except that when the form is submitted, the browser will throw an error if the text inside is not a properly formatted email address. 

```html
<input type="email">
```

### `input[type="password"]`

Again, similar to a text input but changes characters to dots so the password isn't revealed.

```html
<input type="password">
```
### `input[type="search"]`

Again, similar to the text input, but some browsers provide an icon to clear the search box as well as some different styling.

```html
<input type="search">
```

### `input[type="color"]`

A new input in HTML5! This input looks like a color picker. [It's not supported in IE or Opera mini](https://caniuse.com/#feat=input-color), so those browsers will render it as a text input.

```html
<input type="color">
```

### `input[type="submit"]`

This one is technically an input, but you probably think of it as a button. The submit input is the magic button that submits a form and sends the information to the server.

```html
<input type="submit">
```
### `button[type=submit]`

When `<button>Submit</button>` is inside a form element, it acts exactly like `<input type="submit" />`. This means if a user clicks the button, the form will be submitted. For accessibility best practices you should reach for a submit `button` in most cases.

```html
<button type="submit">Submit Form</button>

```
### `button[type=reset]`
If a user clicks this button, all the elements in the associated form will be reset. This means all inputs and text areas in that form will be cleared.

```html
<button type="reset">Reset Form</button>
```

#### `button[type="submit"]` vs. `input[type="submit"]` 

They're largely the same. The only difference is that buttons can have content, because of the opening and closing tags. 

```html
<button>
  <img src="cutepuppy.jpg" alt="really cute puppy in a bath" >
  Click me!
</button>
<!-- vs. -->
<input type="submit" value="Click me!">
```
Use whatever makes most sense for your design.

### `input[type="file"]`

This input allows the user to select a file from their computer.

```html
<input type="file">
```

You can also pass it a `multiple="true"` attribute to allow for multiple file selection:
```html
<input type="file" multiple="true">
```

### `input[type="range"]`

Allows you to implement sliders - handy for when users need to gauge something based on a numerical value. 

```html
<input type="range">
```
You can set the maximum and minimum values using attributes, as well as the step value.

```html
<input type="range" min="30" max="150" step="10">
```

### `input[type="hidden"]`

This is similar to `display:none;`, but safer because the input will still be hidden even if your CSS doesn't load.

Hidden inputs are most often used to store metadata related to the page:

```html
<input type="hidden" value="3Xrg54@Scds!">
```
Sometimes that value means nothing to the user.

## Input attributes
We've talked a bit about attributes specific to the inputs we've seen. Here are some common attributes that many inputs share.

### `name`
Each input should have a name. Sometimes, as with checkboxes (which we'll look at a little further down the page), the same name is used to denote a grouping of inputs. Other times, it's information about what the input is for.

```html
<input type="color" name="themeColor" >
<input type="range" name="favoriteNumber">
```

### `value` 
You can set the default value on any input by setting the `value` attribute. 

```html
<input type="text" value="The honorable">
<input type="color" value="#ff00dd">
<input type="range" value="10">
<input type="submit" value="Send it to the server!">
```
This is also the information that gets sent to the server when the form is submitted.

### `placeholder`
This attribute denotes default text in your input, which clears when a user starts typing. Placeholders are **not** read by screen readers. 

```html
<input type="email" placeholder="Please enter your email address">
```

Notice that it's different from `value`, which doesn't clear.

### `maxlength`
This attribute limits the number of characters an input can take.

```html
<input type="text" placeholder="Please choose a username" maxlength="6">
```

### `required` 

This attribute stops the form from being submitted unless it has been completed. (Before HTML5 we needed to use JavaScript to check if inputs were valid, but now we have the `required` attribute!)

```html
<input type="text" name="firstName" required="true" placeholder="First name">
<input type="text" name="lastName" required="true" placeholder="Last name">
```

### `disabled`

This attribute disables a form element when its value is `true` or when it is included without an equals sign. Disabled elements will not receive focus and therefore will be skipped when a user tabs through them (it will not be read out by a screen reader). The values of disabled elements are not editable and they will not be sent to the server. 

```html
<input type="text" value="I will not get sent to the server!" disabled>
<!-- is the same as writing -->
<input type="text" value="I will not get sent to the server!" disabled="disabled">
```
Add the disabled attribute to an element and you will notice it is grayed out - this is default styling from the browser.

## The `label` element

The `label` element is used to label an input. We can still use regular HTML elements (`p`, `section`, `strong`, etc.) inside forms, but it's best practice to use a label element for form inputs.

A basic form might look like this:

```html
<form action="submit">
  <label for="username">Your Username:</label>
  <input type="text" name="username" id="username">

  <label for="userpass">Password</label>
  <input type="password" name="userpass" id="userpass">

  <input type="submit" value="Log me in!">
</form>
```

We use each input's `id` attribute to connect it to the appropriate label. The `for` attribute exists to make the forms accessible for screen readers. Notice that when we click the label for a checkbox or radio button, it's as though we've clicked the box or button! That's thanks to the connection between the label and the input's `id`.

It's common to see designs where labels are omitted from form elements in favor of placeholders. This is problematic because as soon as a user starts typing in a field, the placeholder disappears, so users no longer have instructions on what the input is for. Also, placeholders will never be read by screen readers. It's important to use labels to ensure all users understand what an input is for before, while, and after they use it.

If you don't have control of the design, still use labels but hide them using a class. Consider the following CSS:

<!-- visually hidden update taken from the a11y project -->
  
```css
.visually-hidden:not(:focus):not(:active) { 
  position: absolute !important;
  height: 1px; 
  width: 1px;
  overflow: hidden;
  clip: rect(1px 1px 1px 1px); /* IE6, IE7 */
  clip: rect(1px, 1px, 1px, 1px);
  white-space: nowrap; /* added line */
}
```

This class will visually hide the content without it being removed from the `DOM` so it is available for screen readers. There are many good use cases for this like hiding labels, adding this class to text which describes icons and hiding headings that are not visually important but help a screen reader navigate the page.

Adding the `:not(:focus):not(:active)` part to the class name means that if the element is interactive and somehow recieves focus, the styles will be undone and the element will be visible. In most cases this is a non-issue and you could instead write:

```css
.visually-hidden { 
  position: absolute !important;
  height: 1px; 
  width: 1px;
  overflow: hidden;
  clip: rect(1px 1px 1px 1px); /* IE6, IE7 */
  clip: rect(1px, 1px, 1px, 1px);
  white-space: nowrap; /* added line */
}
```

It's a good idea to include the `visually-hidden` class in all of your base styles and use it as necessary. Remember to change the class name to adhere to your naming convention, though! You may also see this named `sr-only` for "screen reader only". 

## A word about attributes
It may seem wrong, but sometimes you will have code that looks like this:

```html
<label for="address">Address</label>
<input type="text" name="address" class="address" id="address">
```

That's totally okay! The attributes all have separate purposes!
## The `fieldset` element
The this is a semantic element that groups inputs. Browsers will add a bit of default styling to `fieldset` elements. When you use `fieldset`, you get access to a `legend` element that acts like a label.

```html
<fieldset>
  <legend>Tell us about you!</legend>

  <label for="firstName">First Name</label>
  <input type="text" name="firstName" placeholder="First name here" id="firstName">

  <label for="lastName">Last Name</label>
  <input type="text" name="lastName" placeholder="Last name here" id="lastName">
</fieldset>
```
## More input types
### `input[type="radio"]`
Radio buttons are useful when you want users to select **one thing** from a list of options. We can group them together by giving them the **same name value**.

```html
<fieldset>
  <legend>Select your pizza size:</legend>

  <label for="smallOption">Small</label>
  <input type="radio" name="pizzaSize" value="small" id="smallOption">

  <label for="mediumOption">Medium</label>
  <input type="radio" name="pizzaSize" value="medium" id="mediumOption">

  <label for="largeOption">Large</label>
  <input type="radio" name="pizzaSize" value="large" checked="true" id="largeOption"> 
</fieldset>
```

`checked="true"` will by default select a radio button. You may sometimes also see:

```html
<input type="radio" name="pizzaSize" value="large" checked>
<!-- OR -->
<input type="radio" name="pizzaSize" value="large" checked="checked">
```

Both are valid and work the same as `checked="true"`.

### `input[type="checkbox"]`
Checkboxes are useful when you want users to select as many things as they want from a list of options:

```html
<fieldset>
  <legend>Pizza toppings</legend>

  <label for="olives">Olives</label>
  <input type="checkbox" id="olives" name="topping" value="olives" checked>

  <label for="mushroom">Mushroom</label>
  <input type="checkbox" id="mushroom" name="topping" value="mushroom" checked>

  <label for="bacon">Bacon</label>
  <input type="checkbox" id="bacon" name="topping" value="bacon">

  <label for="sunDriedTomatoes">Sun Dried Tomatoes</label>
  <input type="checkbox" id="sunDriedTomatoes" name="topping" value="sunDriedTomatoes">

  <label for="pineapple">Pineapple</label>
  <input type="checkbox" id="pineapple" name="topping" value="pineapple">
</fieldset>
```
Note how each one has the same `name` attribute but different `value` attributes.
<!-- 
#### Why is my form not sending multiple values for my checkbox inputs?
In some cases, you will need to append a set of square brackets to whatever value you give the name attribute (e.g `name="topping[]"`). The square brackets indicate that the values should be accepted as an <a href="https://www.w3schools.com/js/js_arrays.asp">array</a>. Simply, attaching the square brackets tells your script to accept multiple values for your checkbox inputs. For our example above, we have left out the square brackets - sometimes attaching the square brackets can give you a bit of trouble if you're handling the data using JavaScript (more on JavaScript in our Advanced Web Development course). If you find that the service you are using to submit the form is not handling multiple values as expected, try appending the square brackets to the end of your name value.  -->

### `textarea`

This element is the weird cousin of the input bunch: it's not actually an `input` tag **and** it allows for multiple lines. Also, it requires a closing tag, but no content goes between the tags!

```html
<textarea name="specialInstructions" cols="30" rows="10"></textarea>
```
This element has two new attributes: `cols` and `rows`. These values set the visible width and height of the element (based on average character sizes).

<!-- These attributes are no longer required: we can just use widths and heights, but it's nice to know. -->

### `select`
The `select` element is useful when you want users to select **one thing** from a list of options. The browser usually styles it as a dropdown menu. Unlike radio buttons, the options don't need to share a name, as the `name` attribute is on the parent `select` element. They get their own tag: `option`.

```html
<select name="levelOfSpiciness">
  <option value="noSpice">No Spice</option>
  <option value="mild">Mild </option>
  <option value="medium">Medium</option>
  <option value="spicy">Spicy</option>
  <option value="deathlySpicy" selected>Death.</option>
</select>
```
In the above example, the `value` attribute is what gets sent to the server and the text in between the option tags is what the user sees. To set the default option, use the `selected` attribute. `selected="true"` and `selected="selected"` are also valid.
Note that we cannot use any HTML inside of an option tag.

## The `form` element

The `form` tag takes a number of attributes which specify information about the form. Let's take a look an example contact form:

```html
<form action="sendEmail.php" method="POST" class="applicationForm" autocomplete="off" name="applicationForm">
  <!-- inputs go here -->
</form>
```

1. The value for `action` is the address of a server side file that will handle the information sent to it. In this example, it is a PHP file called `sendEmail.php`. This could be a URL or a relative path. It can also be an action, like `submit`. 
1. The value for `method` is generally `POST` or `GET`, which are two ways of sending information to a server. `POST` is used when sending secure information like passwords. You generally won't need to worry about this until you get into developing with a server side language.
1. Just like any other element, we can add a `class` (or an `id`) to a form.
1. You can apply `autocomplete` to the entire form or a specific input. With the value `off`, the form or inputs won't be autocompleted by the browser. There are also two others called `autocorrect` and `autocapitalize` which you can set to `off` if you are developing for that pesky autocorrecting iPhone.
1. A `name` attribute can be applied to both the form as well as its inputs. It's basically a way of referencing the form when you get into both JavaScript and server side languages.

## Writing CSS for forms

Before we start writing CSS to make our form inputs look a little nicer, let's take a look at a new type of selector that we can use.

In addition to styling inputs by targetting their element type or class:

```css
input {
}

input.emailAddress {
}
```

We can also select them based on their type:

```css
input[type=email] {

}
```
This can be a great selector to use to reset browser defaults.

In addition, we can target trigger styling (i.e. when the user clicks or taps on an element or selects it with the keyboard's "tab" key) by using the :focus state.

```css
input:focus {

}
```

To access the styling of an active input field (i.e. a button element that is clicked by the user), use the :active state.

```css
input:active {

}
```

> **Accessibility tip**
>
> Set element focus with a border or highlight for those who rely on the keyboard navigations.


### Styling `select` elements

Often, in a design, a dropdown will need to be styled beyond the default browser styling for the `select` tag, or it will need a custom dropdown icon. The `select` element (and most other form elements) will need their default browser appearance "turned off" to make styling easier.

Remember that when you remove the default styling, you must create replacement styling for **every state** of an element. This includes `:active` and `:focus`.

```css
select {
  -moz-appearance: none;
  -webkit-appearance: none;
  appearance: none;
  border: 1px solid black;
}
```
With the `appearance` set to `none`, we are free to apply our own styles. The arrow icon will also be removed from the `select` element.

To put your own custom arrow on the select element, we can get creative with a background image. 

```css
select {
  -moz-appearance: none;
  -webkit-appearance: none;
  appearance: none;
  border: 1px solid black;
  background-image: url(http://cdn1.iconfinder.com/data/icons/cc_mono_icon_set/blacks/16x16/br_down.png);
  background-repeat: no-repeat;
  background-position: 95% center;
}	
```

Download [this file](https://hychalknotes.s3.amazonaws.com/resetting-default-select-styles.html) to see the full code.

Styling the options list is essentially not possible at this time. If you are assigned work to customize an options list, you may need to build the list from scratch and implement all of the browser accessibility functionality yourself or reach for a library to help with this task.

### Spotify sign-up form code-along


Let's all try and replicate the Spotify sign-up form! Together we will create the markup and then you will be given time to work on the CSS. Most inputs and forms are just like any other element, so we can use whatever CSS we want on them.  

![spotify sign-up form](https://hychalknotes.s3.amazonaws.com/spotify-sign-up.png)

You can find the starter files [here](https://hychalknotes.s3.amazonaws.com/spotify-form-code-along-STARTER-FILES.zip) and an answer [here](https://hychalknotes.s3.amazonaws.com/spotify-form-code-along-ANSWER.zip).

### Resources and practice
* Here's a [form styling challenge](https://hychalknotes.s3.amazonaws.com/form-styling.zip).
* Recreate Google's [login modal](https://hychalknotes.s3.amazonaws.com/google-login.png) - notice that the placeholder moves [when the input is focused](https://hychalknotes.s3.amazonaws.com/google-login-focused.png). 


