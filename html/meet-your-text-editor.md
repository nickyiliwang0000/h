<!-- Student takeaway -->
<!-- By the end of this lesson, the student should know:
- What syntax highlighting is
- That there are many code editors
- How to edit the user settings in VSCode
- How to add a snippet to VSCode
-->

# Meet your text editor
One of a developer's most important tools is a text editor. The text editor is where a developer does the vast majority of their problem-solving and coding. Using the right text editor with a great setup can make your productivity skyrocket.

HTML is written is plain text, so we could technically use Notepad (Windows) or TextEdit (Mac) to view and edit our HTML files. However, since both programs show nothing but black text on a white background, it's very easy to make a mistake!

Text editors give you something called _syntax highlighting_, which colour-codes your tags to help you quickly scan your code for relevant parts. When you make a mistake, the colour of the tag changes so you can see that something isn't right. Take a look this snippet in Notepad:

![Using Textedit or Notepad](https://hychalknotes.s3.amazonaws.com/notepad-screenshot.png)

Now look at it in a text editor:

![Using a text editor](https://hychalknotes.s3.amazonaws.com/VSCode-screenshot.PNG)

See all the color-formatting and syntax highlighting (the tags are blue, text is white, the current selected tag `<html>` auto-highlights its matching closing tag, etc.)? When your code gets long and nested, little features like these are very helpful for navigating, staying organized and finding errors.

## Choosing a text editor

There are many text editors in the world of development, and each has their own set of features. When choosing a text editor, look for signs that it's easily customizable and has an active development community.

For this bootcamp, we are going to be using [Visual Studio Code](https://code.visualstudio.com/), a free text editor developed by Microsoft. VSCode has been gaining a lot of traction in the industry due to its excellent features, including: 
* syntax highlighting
* intelligent code completion (IntelliSense) 
* snippets
* debugging
* built-in Git GUI

Some other popular text editors currently available are:

* Sublime Text 
  * [http://www.sublimetext.com/3](http://www.sublimetext.com/3)
  * Paid (with unlimited free trial) with extensive customization options. 
  * Widely used

* Atom
  * [https://atom.io/](https://atom.io/)
  * A free, open source text editor from GitHub. 
  * Easily customizable and shares many of the same plugins, features and themes as Sublime.

* Brackets
  * [http://brackets.io/](http://brackets.io/)
  * A free, open source text editor from Adobe. 
  * Easily integrated with other Adobe products (e.g. Photoshop).

* WebStorm 
  * [https://www.jetbrains.com/webstorm/](https://www.jetbrains.com/webstorm/)  
  * Paid, with free trial
  * Integrated Development Environment (IDE) specifically for JavaScript 

* PhpStorm 
  * [https://www.jetbrains.com/phpstorm/](https://www.jetbrains.com/phpstorm/)
  * Paid, with free trial
  * Integrated Development Environment (IDE) specifically for PHP 

## Working with Visual Studio Code 
If you haven't already, head on over to [VSCode's website](https://code.visualstudio.com) to download and install the latest stable build of VSCode.

### Getting started
If you are exploring VSCode for the first time, it's helpful to visit the welcome window at `Help` > `Welcome`. Here, you'll see a few options: you can open a new or recent file or launch the interactive playground (a great place to learn some basic shortcuts!).

![screenshot of visual studio code's welcome page](https://hychalknotes.s3.amazonaws.com/vscodewelcome.png)

Let's take some time to run through some of the interactve playground sections that are relevant to us right now: 
* Multi-cursor editing
* Line actions
* Formatting
* Code folding
* Errors and warnings

Check out these keyboard shortcuts cheatsheets [For Mac](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf) or [For Windows](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf).

### Installing extensions

#### Open-in-browser
This extension will allow you to use a shortcut to preview your HTML files in your default browser.
  
  1. Type in `cmd + shift + p` or `ctrl + shift + p` and type `install`. Pick 'Extensions: Install Extension'.
  2. Type `open in browser`. Most of the available packages are very similar. The one by `coderfee` has been popular with HY students. Install whichever one you want by hitting 'Enter'.
  3. Restart Visual Studio Code 
  4. Open HTML files in default browser by pressing `alt + b` or right clicking and selecting 'Open in Default Browser'.

### Make it look good

VSCode, like many other text editors, gives us the ability to customize the appearance of our working files. There are a few default themes installed. To switch your theme, go to 'Code > 'Preferences' > 'Color Theme' or use the shortcut `cmd + K cmd + T` (Mac) / `ctrl + K ctrl +T ` (Windows) to launch a window with the pre-installed options. You can also select `Install Additional Color Themes` which will launch the 'Extensions' panel with infinite options available for you to install and check out. You can switch your theme up as much as you like - eventually you will be so busy you'll forget to change it and that'll be the one you have forever. 

Some staff favourites are `Oceanic Next`, `Material Theme`, `Material Dark`, and `Cobalt 2`.

### Edit user settings 

It's worthwhile to spend a bit of time customizing your text editor since you will be spending so much time with it. You can override defaults in your user settings file which can be found at 'Code' > 'Preferences' > 'Settings' or via the shortcut `cmd + ,` (Mac) or `ctrl + ,` (Windows). You can play around with the visual interface provided or you can customize the settings in JSON.

To access your `settings.json` file, select the `Extensions` option in your Settings window. You should see a link that says `Edit in settings.json`. Another option is to type `command + shift + p` and type in `Open Settings (JSON)`. 

The _JavaScript Object Notation_ (JSON) format is a data format that, despite its name, is language-independent. (Though we will be seeing it again when we get into JavaScript.) JSON's syntax uses key-value pairs that are separated by commas, with a colon between they key and the value, like this: 

```json
{
  "setting 1" : "On Wednesdays we have Salad Club"
}

```

Right now, your settings file might be empty or only contain the rules that define the theme you selected. Eventually you might have your own list of settings that work for you, but for now here are some that you might enjoy! 

```json
{
  "editor.minimap.enabled": false,
  "editor.wordWrap": "on",
  "editor.formatOnPaste": true,
  "emmet.includeLanguages": {
      "javascript" : "javascriptreact"
  }
}
```

There are some things to note about the above syntax. The last key-value pair on the list has no trailing comma. All keys and most values are wrapped in **double quotes**. The exceptions are when you are using numbers:

```json
{
  "editor.tabSize": 2
}
```

Or when the value some key is set to `true` or `false` (we call these values _boolean_ values). 

```json
{
  "editor.formatOnPaste": true
}
```

## Snippets

_Snippets_ make your workflow much faster. A snippet is a chunk of code that you can insert into your file using a shortcut and the `tab` key. Lots of people use snippets for boilerplate code.

To create a new snippet in Visual Studio Code:
* Mac: go to 'Code' > 'Preferences' > 'User Snippets'
* Windows: go to 'File' > 'Preferences' >'User Snippets'

You can also do this through the command pallet by typing `cmd + shift + p` (Mac) or `ctrl + shift + p` (Windows) and type `snippets`. Pick `Preferences: Configure User Snippets`.

Snippets are scoped to specific languages, so you will need to select the language in which you'd like the snippet to be available to you.

Let's choose HTML and write our first snippet! 

### Writing snippets 
Just like the user settings file, snippets are written in JSON. All snippets live inside of one large object denoted by curly braces `{}`. Each snippet is defined by a name and has a prefix, body, and description. 

Let's start by adding a snippet to our `html.json` file. **Inside the parent curly braces(!)**, enter the following:

```json
//html.json
"jQuery CDN": {
  "prefix": "jquery",
  "body": "<script src='https://code.jquery.com/jquery-3.2.1.min.js' integrity='sha256-hwg4gsxgFZhOsEEamdOYGBf13FyQuiTwlAQgxVSNgt4='crossorigin='anonymous'></script>",
  "description": "jquery 3.x"
}
```

The above snippet will allow us to easily include a link to the jQuery CDN in any HTML file. If you get an error, check the bottom left of the editor window - there are icons for errors and alerts that will help you figure out what went wrong (probably an errant curly brace!).

Now create a new HTML document, type `jquery` + `tab`, and see that you get the whole jQuery snippet!

To add another snippet, add another object below the `jQuery CDN` one. After the closing curly brace of your first snippet, **add a comma**, then on a new line add this snippet to quickly include the viewport `meta` tag for responsive web pages: 

```json
"Viewport": {
  "prefix": "responsive",
  "body": "<meta name='viewport' content='width=device-width, initial-scale=1'>",
  "description": "viewport meta tag"
}
```

### Multi-line snippets
Notice how each of the above snippets is wrapped in double quotes? This is perfectly fine for one-line snippets, but if you want to create a multi-line snippet you need to put it in square brackets like so:

```json
"Multi-line Snippet" : {
  "prefix": "hi",
  "body" : [
    "<div>",
    "\t<h2>$1</h2>",
    "\t<p>$2</p>",
    "</div>"
  ],
  "description": "Div with an h2 inside of it"
}
```
Each line in a multi-line snippet is wrapped in quotes and comma separated. If you want to include tabs, you can do so by inserting `\t`. Notice the `$1` & `$2`?  You can insert placeholders into your snippets by using this syntax which will move your cursor to a specific area where you might want to input some text.  Once you press tab, it will jump to the next one!

### Your snippet library
Now that we've written some of our own snippets, we can quickly add the following CSS snippets to our `css.json` file and `scss.json` file so they are available in both file formats. 

We're going to add: 
1. Border-box
2. Normalize
3. Clearfix
4. VisuallyHidden
5. SR-Only
6. Setup (a snippet that includes all of the above!) 

Find the CSS snippet file by typing `cmd + shift + p` on Mac or `ctrl + shift + p` on PC to launch the command palette and type in `snippets`. Select the option 'Preferences: Configure User Snippets' and choose the language you want to use your snippets in (for these snippets, CSS). 

Inside of this `css.json` file, paste the following code:

```json
"Border-box": {
  "prefix": "bor-box",
  "body": "* { -moz-box-sizing: border-box; -webkit-box-sizing: border-box; box-sizing: border-box; }",
  "description": "Box Sizing Snippet"
},

"Normalize": {
        "prefix": "normalize",
        "body": [
            "html{line-height:1.15;-ms-text-size-adjust:100%;-webkit-text-size-adjust:100%}body{margin:0}article,aside,footer,header,nav,section{display:block}h1{font-size:2em;margin:.67em 0}figcaption,figure,main{display:block}figure{margin:1em 40px}hr{box-sizing:content-box;height:0;overflow:visible}pre{font-family:monospace,monospace;font-size:1em}a{background-color:transparent;-webkit-text-decoration-skip:objects}abbr[title]{border-bottom:none;text-decoration:underline;text-decoration:underline dotted}b,strong{font-weight:inherit}b,strong{font-weight:bolder}code,kbd,samp{font-family:monospace,monospace;font-size:1em}dfn{font-style:italic}mark{background-color:#ff0;color:#000}small{font-size:80%}sub,sup{font-size:75%;line-height:0;position:relative;vertical-align:baseline}sub{bottom:-.25em}sup{top:-.5em}audio,video{display:inline-block}audio:not([controls]){display:none;height:0}img{border-style:none}svg:not(:root){overflow:hidden}button,input,optgroup,select,textarea{font-family:sans-serif;font-size:100%;line-height:1.15;margin:0}button,input{overflow:visible}button,select{text-transform:none}button,html [type=button],[type=reset],[type=submit]{-webkit-appearance:button}button::-moz-focus-inner,[type=button]::-moz-focus-inner,[type=reset]::-moz-focus-inner,[type=submit]::-moz-focus-inner{border-style:none;padding:0}button:-moz-focusring,[type=button]:-moz-focusring,[type=reset]:-moz-focusring,[type=submit]:-moz-focusring{outline:1px dotted ButtonText}fieldset{padding:.35em .75em .625em}legend{box-sizing:border-box;color:inherit;display:table;max-width:100%;padding:0;white-space:normal}progress{display:inline-block;vertical-align:baseline}textarea{overflow:auto}[type=checkbox],[type=radio]{box-sizing:border-box;padding:0}[type=number]::-webkit-inner-spin-button,[type=number]::-webkit-outer-spin-button{height:auto}[type=search]{-webkit-appearance:textfield;outline-offset:-2px}[type=search]::-webkit-search-cancel-button,[type=search]::-webkit-search-decoration{-webkit-appearance:none}::-webkit-file-upload-button{-webkit-appearance:button;font:inherit}details,menu{display:block}summary{display:list-item}canvas{display:inline-block}template{display:none}[hidden]{display:none}"
        ],
        "description": "CSS Normalize Snippet"
    },

"Clearfix": {
  "prefix": "clearfix",
  "body": " .clearfix:after {visibility: hidden; display: block; font-size: 0; content:''; clear: both; height: 0; } ",
  "description":"Clearfix Snippet" 
},

"VisuallyHidden": {
  "prefix": "vhidden",
  "body": ".visuallyHidden:not(:focus):not(:active) { position: absolute; width: 1px; height: 1px; margin: -1px;border: 0;padding: 0;white-space: nowrap;clip-path: inset(100%);clip: rect(00 0 0);overflow: hidden;}",
  "description": "Visually Hidden Snippet"
},
"sr-only": {
        "prefix": "sr-only",
        "body": ".sr-only { position: absolute; width: 1px; height: 1px; margin: -1px; border: 0; padding: 0; white-space: nowrap; clip-path: inset(100%); clip: rect(0 0 0 0); overflow: hidden;}",
        "description": "sr-only Snippet"
    },

"Setup": {
  "prefix": "setup",
  "body": [
  "a,abbr,acronym,address,applet,article,aside,audio,b,big,blockquote,body,canvas,caption,center,cite,code,dd,del,details,dfn,div,dl,dt,em,embed,fieldset,figcaption,figure,footer,form,h1,h2,h3,h4,h5,h6,header,hgroup,html,i,iframe,img,ins,kbd,label,legend,li,mark,menu,nav,object,ol,output,p,pre,q,ruby,s,samp,section,small,span,strike,strong,sub,summary,sup,table,tbody,td,tfoot,th,thead,time,tr,tt,u,ul,var,video{margin:0;padding:0;border:0;font-size:100%;font:inherit;vertical-align:baseline}article,aside,details,figcaption,figure,footer,header,hgroup,menu,nav,section{display:block}body{line-height:1}ol,ul{list-style:none}blockquote,q{quotes:none}blockquote:after,blockquote:before,q:after,q:before{content:'';content:none}table{border-collapse:collapse;border-spacing:0}input[type=search]::-webkit-search-cancel-button,input[type=search]::-webkit-search-decoration,input[type=search]::-webkit-search-results-button,input[type=search]::-webkit-search-results-decoration{-webkit-appearance:none;-moz-appearance:none}input[type=search]{-webkit-appearance:none;-moz-appearance:none;-webkit-box-sizing:content-box;-moz-box-sizing:content-box;box-sizing:content-box}textarea{overflow:auto;vertical-align:top;resize:vertical}audio,canvas,video{display:inline-block;max-width:100%}audio:not([controls]){display:none;height:0}[hidden]{display:none}html{font-size:100%;-webkit-text-size-adjust:100%;-ms-text-size-adjust:100%}a:focus{outline:thin dotted}a:active,a:hover{outline:0}img{border:0;-ms-interpolation-mode:bicubic}figure{margin:0}form{margin:0}fieldset{border:1px solid silver;margin:0 2px;padding:.35em .625em .75em}legend{border:0;padding:0;white-space:normal}button,input,select,textarea{font-size:100%;margin:0;vertical-align:baseline}button,input{line-height:normal}button,select{text-transform:none}button,html input[type=button],input[type=reset],input[type=submit]{-webkit-appearance:button;cursor:pointer}button[disabled],html input[disabled]{cursor:default}input[type=checkbox],input[type=radio]{box-sizing:border-box;padding:0}input[type=search]{-webkit-appearance:textfield;-moz-box-sizing:content-box;-webkit-box-sizing:content-box;box-sizing:content-box}input[type=search]::-webkit-search-cancel-button,input[type=search]::-webkit-search-decoration{-webkit-appearance:none}button::-moz-focus-inner,input::-moz-focus-inner{border:0;padding:0}textarea{overflow:auto;vertical-align:top}table{border-collapse:collapse;border-spacing:0}button,html,input,select,textarea{color:#222}::-moz-selection{background:#b3d4fc;text-shadow:none}::selection{background:#b3d4fc;text-shadow:none}img{vertical-align:middle}fieldset{border:0;margin:0;padding:0}textarea{resize:vertical}.chromeframe{margin:.2em 0;background:#ccc;color:#000;padding:.2em 0}",
  "",
  ".clearfix:after {visibility: hidden; display: block; font-size: 0; content: ''; clear: both; height: 0; }",
  "",
  "* { -moz-box-sizing: border-box; -webkit-box-sizing: border-box; box-sizing: border-box; }",
  "",
  ".visuallyHidden:not(:focus):not(:active) { position: absolute; width: 1px; height: 1px; margin: -1px;border: 0;padding: 0;white-space: nowrap;clip-path: inset(100%);clip: rect(00 0 0);overflow: hidden;}"
  ],
  "description": "Reset, Border-Box, Clearfix and Visually Hidden"
}
```
Repeat the above steps for `scss.json`.

Keep in mind that the above `setup` snippet includes four different rule sets, and you might not need all for every project. Be mindful of this, and either use the individual snippets when you don't need all, or if you use `setup`, make sure to delete the sections you don't need out of your CSS.

You should now have access to the following snippets in HTML: 

* `jquery` + `tab`
* `responsive` + `tab`

And the following snippets in CSS/SCSS: 

* `bor-box` + `tab`
* `normalize` + `tab`
* `clearfix` + `tab`
* `vhidden` + `tab`
* `sr-only` + tab
* `setup` + `tab`

Don't stop here - feel free to make your own! If you need help, there's a handy [snippet generator](https://snippet-generator.app/) that will format your snippets for you.

### Learn more

There are a lot of built in shortcuts in VSCode to make your coding experience more efficient. Some of our favourites include: 

* `option + [arrow up or down]` (Mac) or `alt + [arrow up or down]`(PC) : moves a line of code up or down
* `option + cursor click` (Mac) or `alt + cursor click` (PC): creates multiple cursors to allow for faster code editing
* `command + b` (Mac) or `ctrl + b` (PC): opens and closes the file navigator panel
* `command + d` (Mac) or `ctrl + b` (PC): highlight matching keywords in a file
* `command + shift + k` (Mac) or `ctrl + shift + k` : delete an entire line of code
* `command + ctrl + space bar` (Mac) or `window key + .` (PC): to access the very important Emoji keyboard!


Some instructor favorite setups include:
* 'View' > 'Editor Layout' > 'Two Columns' will give you two panes in which to open files - perhaps the HTML and CSS for the same project, instead of putting them in tabs?
* If you've got a Mac, open the command palette (`cmd + shift + p`, type `shell command` and select 'Install code command in PATH' ![shell command screenshot](https://code.visualstudio.com/assets/docs/setup/mac/shell-command.png)

  Now you'll be able to type `code .` in a file in the command line and have it open in VSCode! PC users are lucky -  this is built in for them!

We'll be learning more about this text editor as the course goes on and features become useful to us. If you're keen to take an even deeper dive, you can check out these [intro videos](https://code.visualstudio.com/docs/getstarted/introvideos)! 

