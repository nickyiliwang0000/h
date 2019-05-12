## jQuery Documentation

### Reading jQuery API documentation

jQuery objects have tons of methods, but lucky for us, they're extremely well documented and always available at [api.jquery.com](http://api.jquery.com).

This is something you should get used to having to look up; even seasoned developers do it! The best way to find out what a method does, is to _read about what it does_. 

#### If you're not sure what method to use

Take a look at the side panel on [api.jquery.com](http://api.jquery.com). This is a really great categorization of all the various methods.  See if what you want fits into one of these categories.

**Example**

How do select a DOM element with jQuery?

Things like `Ajax`, `CSS`, and `Deprecated` don't look like they fit the bill, but keep going and you'll see `Selectors`.  That sounds promising, so let's look at a sub-category like `Basic`. You'll see some familiar methods like the Class Selector. From here you can explore an individual method to see if it does what you want. For example, the docs for Class Selector say it "Selects all elements with the given class." 

If it doesn't seem like what you want, head back up the categories list and try again!

You can also try searching if you have a vague idea of what you want. For example, a search for `class` returns results for Class Selector, the `.addClass()` method, etc.

If you're really, really stuck on which method to use, you can also google "how to do x with jQuery" and will probably find an answer that points you to the right method.

#### To find out how to use a method

When you think you know what method you want, take a look at it's page in the docs to find out how to use it.

For example, if we want to replace the inner HTML of a DOM node but aren't sure of which method to use, we can Google `jQuery replace inner HTML` and one of our first results should be the jQuery documentation page for the `.html()` method. 

Let's look at [the documentation](https://api.jquery.com/html/) for the `.html()` method to see how we can change the text inside an `h1` tag.

1. Check to make sure the **Description** matches what you're trying to accomplish. Note that some methods are **getters and setters** - meaning they can do two different things. The first way that `.html()` is described is it will '**Get** the HTML...'. You may have to scroll down to see the right one. In our example, we want to change the text, so move down to the section that says "**Set** the HTML contents..." 

	![A screenshot of the jQuery documentation page for the .html method that accepts an argument description, reading: "Description: Set the HTML contents of each element in the set of matched elements."](https://i.cloudup.com/VWmTxZ1eOT-1200x1200.png)

2. Look at the **syntax** description to see what arguments (if any) your method takes.
In this case, it takes one argument, `htmlString`. Also, there is an alternate way to call the `.html()` method by passing a function into it.

	![A screenshot of the description of the type of argument the .html method will accept, reading "A string of HTML to set as the content of each matched element."](https://i.cloudup.com/HfrGuwa5ME-3000x3000.png)


A lot of methods can take different types or amounts of arguments, so pick the method that's best suited to what you need and figure out what kind of argument it takes. When in doubt, clicking the linked text in the type will bring you to a page that explains what the method is looking for. 

3. When in doubt, scroll down to find an **example** of this method in practice!

![A screenshot of the jQuery documentation showing a functioning example of using the .html method, replacing an inner div with a paragraph element](https://hychalknotes.s3.amazonaws.com/htmlmethodexample.png)

#### Exercise 

Download and open up [**jquery-docs.html**](https://hychalknotes.s3.amazonaws.com/jquery-docs.html) and use the jQuery API Documentation to complete the exercise. The answer can be found at [**jquery-docs-answer.html**](https://hychalknotes.s3.amazonaws.com/jquery-docs-answer.html).

Explore some methods in the following categories and give them a try on your own.

- document traversal
- DOM manipulation
- events
- effects/animations
- attributes
