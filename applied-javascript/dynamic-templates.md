## Dynamic Templates in JS

### Dynamic Templates

You might find that as your app grows over time, using jQuery to build and concatenate your markup will get very messy and unruly. Thankfully there are libraries out there that allow us to write nice templates for use to use and make this easier!

When you build apps using a JavaScript framework like Angular, Ember or Backbone you don't create elements like this:

```js
var $container = $('<div>');
var $img = $('<img>').attr('src','...');
$container.append($img);

$('#students').append($container);
```

Frameworks use a templating library to make this process more elegant. In fact the library we are going use (Handlebars), is used by [Ember.js](http://emberjs.com/).

#### Templates?

What does a template look like? We will be using the Handlebars templating library to create our templates. In Handlebars, a template looks like this:

```html
<div class="student">
	<h3>{{name}}</h3>
	<p>{{cohort.season}} {{cohort.year}}</p>
	<img src="{{photo}}" />
</div>
```

Looks a lot like HTML! You will also notice the `{{...}}` syntax. This is what Handlebars calls an expression. Inside of these expressions, we use keys from an object to tell Handlebars what we want to display there. Consider the above template with this object:

```js
var student = {
	name: 'Joe Smith',
	cohort: {
		season: 'Fall',
		year: 2014
	},
	photo: 'http://photo.com/image/joe_smith.jpg'
}
```

This will produce the following markup:

```html
<div class="student">
	<h3>Joe Smith</h3>
	<p>Fall 2014</p>
	<img src="http://photo.com/image/joe_smith.jpg" />
</div>
```

#### Using Handlebars

So how do we actually work with Handlebars? First we need to include the library on the page. We will use a CDN link for ours, <https://cdnjs.cloudflare.com/ajax/libs/handlebars.js/4.0.5/handlebars.min.js>.

Create an `index.html` file and a `script.js` file. In the `head`, link up Handlebars and jQuery.

Then we need to set up our first template. To do this we will use a `<script>` tag. (This can be inside of the `head` or `body` tag.)

```html
<script id="myTemplate" type="x-handlebars-template">
	<p>{{name}}</p>
</script>
``` 

In this tag we put any HTML that we want and our first expression. In this case it is simply and expression that wants to print out a name. The first thing we need to do is collect the HTML from the template.

**STEP 1**

```js
var myTemplate = $('#myTemplate').html();
```

The next thing we need to do it to is compile the template. We use the `Handlebars.compile` method to do this: that method will take the HTML from the template and convert it to something that Handlebars recognizes.

**STEP 2**
```js
var myTemplate = $('#myTemplate').html();
var template = Handlebars.compile(myTemplate);
```

The third step involves passing some data to the newly compiled template. We store the data in a new variable so that we can append it later.

**STEP 3**
```js
var myTemplate = $('#myTemplate').html();
var template = Handlebars.compile(myTemplate);

var person = {
	name: 'Joe Smith'
};

var personTemplate = template(person);
```

The final step is appending it to the page!

**STEP 4**
```js
var myTemplate = $('#myTemplate').html();
var template = Handlebars.compile(myTemplate);

var person = {
	name: 'Joe Smith'
};

var personTemplate = template(person);

$('#person').append(personTemplate);
```

#### Handlebars helpers.

So what if you have an object that looks something like this:

```js
var student = {
	name: 'Joe Smith',
	course: ['Bootcamp', 'Part Time Ruby on Rails', 'Javascript'],
	photo: null,
	age: 27
}
```

In this object we have an array of courses and no student photo (Editor's note: I guess Joe Smith doesn't go to Juno). Lucky for us, Handlebars has a way for us to work with arrays and conditions.


#### each

```html
<script id="template" type="text/x-handlebars-template">
    <div>
		<h2>{{name}}</h2>
	  	<ul>
	    {{#each course}}
	      	<li>{{this}}</li>
	    {{/each}}
	  	</ul>
    </div>
</script>
``` 


The `each` helper is a lot like `$.each` from jQuery. It allows us to loop through an array. In our case the array is the `course` array on our `student` object.

Since this is just an array and not an array of object, we can use `this` to print the elements to the page! If there was an object we could just use the key names from the objects.

#### if 

The second helper we will look at is `if`. It is used to conditionally render a section. It checks to see if the value is `false`, `undefined`, `null`, `""`, `0`, or `[]`. In the case of our `student` object, the photo is set to null. So if we wanted to show a student image only if the image key had a value, we could use the `if` block.

```html
<script id="template" type="text/x-handlebars-template">
    <div>
		<h2>{{name}}</h2>
	  	<ul>
	    {{#each course}}
	      	<li>{{this}}</li>
	    {{/each}}
	  	</ul>
	  	{{#if photo}}
        	<img src="{{photo}}" alt="" />
      	{{/if}}
    </div>
</script>
```

Similar to the `each` helper we can say `if photo`, and it will only go into that block if there is a photo.

Download these exercises <a href="https://hychalknotes.s3.amazonaws.com/dynamic_templates_exercise.zip" class="exercise">files</a> and let's try an example.

 
