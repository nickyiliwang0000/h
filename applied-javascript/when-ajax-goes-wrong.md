<!-- Student takeaways: -->
<!-- At the end of this lesson, the student will be able to:
- Open and understand the network tab in the dev tools
- Use other console statements beside 'log'
- Understand what a 'breakpoint' and 'debugger' statement are
- Step through a simple codebase with the debug tools
- Understand the value of the scope tab in the debugger pane
-->
## Debugging in JavaScript
In general, when debugging Javascript it is best to follow these simple principles:

1. Be methodical
2. Try to narrow down when a bug is happening
3. Only change one thing at a time
4. Take breaks

There are also many tools that will help in the debugging process, we are going to explore a few.

### Console statements
By far the most used debugging tool in Javascript is the `console.log` statement. It is wonderful, but there are other console methods that can be used in certain situations that will make your debugging life easier.

- `console.table`: Will print an array or object formatted as a table. This can be useful when trying to parse through large objects or arrays.
- `console.group` and `console.groupEnd`: These two methods should be used together. They will group any console statement between them together. This can allow you to hide/show certain groups of console statements for less visual clutter
- `console.trace`: This prints what is called a *stack trace*. This is basically a timeline of all the functions that were called until you got to the function you are currently in. This can be useful in code bases you are not familiar with to understand what functions are calling what other functions.
- `console.dir`: Calling this with a DOM node will result in the dom node being printed as an object instead of as the markup. This can make looking through properties of a DOM node easier.

### Debugging in the browser
The Browser Dev Tools have a whole set of aids that can assist in the debugging process. To find these tools, do the following:

1. Open up your dev tools
2. Dock your dev tools so they sit at the bottom of the page and make your browser as wide as possible
3. Click on the Debugger tab (note in Chrome this tab is called Sources)

This will open up a panel with a whole host of options. In practice working with them, download [this set of files](https://hychalknotes.s3.amazonaws.com/debug.zip). Note, step 2 is not mandatory for the debugger to work but gives the best overall view of the debugger tools.

![](https://hychalknotes.s3.amazonaws.com/Screen%20Shot%202020-03-30%20at%2011.11.39%20AM.png)
When you open the debugger pane, you will see the above screen. On the far left you will find the `Sources` pane. Here Firefox will display all the files that it is running. You may have some extensions that are running Javascript code, they will appear here as well. In order to de-clutter this area, you can right click on the root folder of the project we just downloaded and set it as the root directory. Now we will only see the `index.html` and `script.js` that contain the code for this project.

![Adding breakpoints](https://hychalknotes.s3.amazonaws.com/breakpoint.gif)

Beside the `Sources` pane, in the middle of the debugger panel, you can view the code based on whatever file is selected in the `Sources` panel. In this area you can add *breakpoints* to your code. A breakpoint is a temporary indication to the browser that the execution of the code should pause at that point so that you can have a look at what might be happening in that exact moment with your program. You can add breakpoints manually to specific lines in your program by clicking on the line numbers. Doing this will cause a blue chevron-like shape to appear at that line number, clicking again will remove it.

You can also add more general breakpoints for event listeners firing, XHR (another word for API requests) being made or DOM manipulation happening. All of these settings are found in the `Breakpoints` panel on the left side of the debugger pane. 

### Using breakpoints
Try setting a breakpoint on line 13 and clicking the button on the page.

Your code will now run up until that line of code and then pause. You can now inspect what is going on in the thread of execution for your code. On the right side, collapse the Breakpoints pane. Underneath it there are two other windows.

![](https://hychalknotes.s3.amazonaws.com/Screen%20Shot%202020-03-30%20at%2011.21.22%20AM.png)

One of these sections is called `Callstack` and the second is called `Scopes`. The Callstack window displays the functions that are currently in line to be executed by JavaScript. The Scope pane displays all the variables that are currently defined in your program and their values at this current moment. You can think of this section as if you have added a `console.log` for every single variable in your program. A note, some of these options will not be viewable unless you have breakpoints set.

### Navigating through your program
Now that we have paused the thread of execution on the breakpoint, we can step through the rest of the code in several different ways. To do this, use the controls pictured below.

![](https://hychalknotes.s3.amazonaws.com/Screen%20Shot%202020-03-30%20at%2010.56.12%20AM.png)

- The first button: *resume* will continue the execution of the program until the next breakpoint or the end of the code is reached.
- The second button: *step over* will execute the next function after the breakpoint and then stop
- The third button: *step into* will go inside of a function
- The fourth button: *step out of* will exit a function to where it is being called
- The final button allows you to deactivate all your breakpoints with one click

Using these controls, you can walk through your code checking specific lines of code that you think might be causing a problem. While you are using these controls to step through your code, the variables in scope, are available to you in your console. You can use them to further understand how you might fix a potential bug.

### Debugger statement
If you want to add similar functionality to a breakpoint directly into your code, you can do so using the keyword `debugger`. When added into your code, this will cause the execution thread to pause. In Firefox and Chrome, the Dev tools must already be open in order for the `debugger` statement to trigger. This is a safe guard in case you accidentally put a `debugger` statement on a live site!

### Try it!
In our code, the `add` function is not working correctly. 

Using the debugging tools, try to pinpoint the line on which this bug is being created. 
Try the following:
- Add a breakpoint for when the button is clicked
- Add a breakpoint to the `<section>` when its children nodes are edited
- Practice stepping into each function
- Practice stepping over functions that don't seem important to the bug
- Explore the values of variables in each of the functions
- Add a `debugger` statement somewhere in the `script.js` code

### This seems like a lot of work, why not just use `console.log`? 
Logging information to the console is a great tool that you will definitely use a lot. However, for code bases where you are not familiar with the flow of the code or code bases that you are revisiting and have forgotten what the code does, the debugger tool is a great way to be able to step through code and understand what is calling what. Another advantage to the debugger is that it gives you access to all the value of all of your variables. So if you forget to console log one important piece, you don't have to go back and add the console log and run all your code again. You can just use the sources pane in the debugger to check what the value of a given variable is at a certain point. 

There are many more features in the debugger including setting conditional breakpoints and watching certain expressions. However, we want to start getting comfortable navigating the above tools. As you get more comfortable using these parts of the debugger, feel free to keep exploring!

VSCode also has a debugger built right into your code editor. You will need to install an add an add on like `Debugger for Firefox` or `Debugger for Chrome`  on in order to be able to debug browser code.

### Seeing AJAX requests

It's often useful to see what the browser is doing behind the scenes when we're making AJAX requests. Luckily, dev tools can help us here.

1. Open up your dev tools

2. Click on the Network tab

3. Click the filter icon to choose which requests show up in this panel. You'll notice stylesheets, scripts and images also show up here. Choose XHR to limit the view to AJAX requests only.

Chrome

![network filter on chrome](https://hychalknotes.s3.amazonaws.com/network-filter-chrome.png)


Firefox 

![network filter on firefox](https://hychalknotes.s3.amazonaws.com/network-filter-firefox.png)

4. Refresh the page to start capturing requests in the Network panel.

5. Clicking on a request will take you to a panel where you can see the response header, response/body, etc.

Using the information here will help tremendously in debugging AJAX requests. If you don't see your request at all, check for things like syntax errors. If the request was made but the result wasn't as expected then have a look at the headers and body of the response.
