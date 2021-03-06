<!-- Student takeaway: -->
<!--Student will be able to:
- Find and use the dev tools in any browser
-->
# Developer tools

Developer tools are the secret weapon of any web designer or developer. Without them, the web would look a whole lot worse. 

Every browser has its own set of dev tools - Chrome and Firefox have some of the most powerful, but Safari, Opera, and IE have their own, too. They are all a little different but they do generally the same thing, you'll probably have to learn how to use them all when you start debugging in each browser. 

Our dev tools are packed with tons of helpful little tools for developing a website, we are going to take a look at the most common use of inspecting elements. By now you may be pulling your hair out wondering how someone can know which CSS rule applies to which element(s). The good news is that we aren't **that smart** - we use dev tools to help us with this.

## Trying dev tools
Download [devTools-exercise.zip](https://hychalknotes.s3.amazonaws.com/devTools-exercise--bootcamp.zip). Unzip the files and open up the index.html file in your browser.
Let's right-click our page and select 'Inspect Element'. This brings up two panels:

![screenshot of developer tools in a browser](https://hychalknotes.s3.amazonaws.com/browserToolsScreenShot.png)

On the left you will see the markup and on the right you will see the CSS that applies to the element you selected.

### Editing a selector
Notice that the first letters of all the words in the header elements are capitalized? Click the **cursor within a square** icon (top left corner) and then click the teal "Summer School Learning" title. You'll see the CSS rule which is formatting the headers - `text-transform: capitalize`. Go ahead and try to change the colour or font size. You can even add new properties like `border:2px solid green;`

### Playing with dev tools
Here are a bunch of tasks to get comfortable with dev tools. When you're done, we'll go through some of the ones you had trouble with.

1. Decrease the padding on the `<div class="titleText">` and add a purple border.
2. Change the `<body>` background colour to something you like better.  
  * Hint: You can click the white square to reveal the colour picker.
3. Increase the padding of the `<div class="description">` and add 20px of margin to the top of it.
3. Select any `<p>` and make the font size 35px.
4. Double click any text element and change the text!
5. Take any margin off all the H2 tags.

As you can see, dev tools are very helpful for figuring out which styles are being applied to which elements as well as quickly testing new styles on existing elements. We will be using dev tools throughout the entire course to please **don't hesitate to ask questions about it**!

### Dev tools exercise
This exercise will encourage you to explore the dev tools in your own way and have a bit of fun doing it!

1. Go to a website of your choice. 
2. Using the dev tools, alter some of the content, images, or styles - be creative!
3. Take a screenshot.
4. Post the screenshot to our Slack channel.
5. Everybody laughs.

Here is an example:

![A screen shot of a news sites headline altered using the dev tools. The headline reads "Researchers discover first case of Emo dating back to 1985" and the tagline reads "World renowned know-it-all Bill Nye unearths new evidence corroborating the widely speculated theory that Will Smith is Emo."](https://hychalknotes.s3.amazonaws.com/screenShotExample.png)

If you need a point in the right direction, here's a short list of websites with plenty of content to change:

- [New York Times](https://www.nytimes.com/)
- [Nature](https://www.nature.com/news)
- [NPR](https://www.npr.org/)
- [The White House](https://www.whitehouse.gov/)
- [NASA](https://www.nasa.gov/)
- [Reddit](https://www.reddit.com/)

