## Snippets - Visual Studio Code

Snippets make your workflow much faster. By typing a small shortcut and hitting <kbd>tab</kbd> we can expand that into some really good boiler plate code.

To create a new snippet in Visual Studio Code, go to `code` > `Preferences` > `User Snippets`. Snippets are scoped to specific languages, so you will need to select the language in which you'd like the snippet to be available to you. 

Let's choose `HTML` and write our first snippet! 

### Writing Snippets 
Just like the user settings file, snippets are written in `JSON` (JavaScript Object Notation). All snippets are composed inside of one large object denoted by curly braces`{}`. Each snippet is defined under a snippet name and has a prefix, body and description. 

Let's start by adding a snippet to our `html.json` file. Inside the parent curly braces, enter the following: 
```json
	"jQuery CDN": {
	    "prefix": "jquery",
	    "body": "<script src='https://code.jquery.com/jquery-3.2.1.min.js' integrity='sha256-hwg4gsxgFZhOsEEamdOYGBf13FyQuiTwlAQgxVSNgt4='crossorigin='anonymous'></script>",
	    "description": "jquery 3.x"
}
```
**If you get an error** check the bottom left of the editor window - there are icons for errors and alerts that will help you figure out what went wrong. (Probably an errant curly brace!)

The above snippet will allow us to easily include a link to the jQuery CDN in any html file. One thing to note is that you will need to use a mix of single quotes and double quotes in the body of the snippet or 'escape' the quotes by adding a `/` before any quote you want to be a part of the body, not a closing quote. 

If you want to add another snippet, you can do so by adding another object below this one. After the closing curly brace on a new line, add this snippet to quickly include the viewport meta tag for responsive webpages: 

```json

"Viewport": {
	"prefix": "responsive",
	"body": "<meta name='viewport' content='width=device-width, initial-scale=1'>",
	"description": "viewport meta tag"
}
```
With these snippets, all we now need to do is type the prefix defined above and hit tab and it will spit out the code defined in the body.

### Multi Line Snippets
Notice above how each snippet is wrapped in double quotes? This is perfectly fine for one line snippets, but if you want to create a multi-line snippet you need to put it in square brackets like so:

```json
 	"Multi-Line Snippet" : {
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

Now that we've gone through writing our own snippets, we can quickly add the following css snippets to our `css.json` file and `scss.json` file so they are available in both file formats. 

We're going to add: 
1. Normalize
2. Border Box
3. Clearfix
4. Setup (a snippet that includes all of the above!) 

Find the css snippet file by typing `CMD + Shift + P` on Mac or `Ctrl + Shift + P` on PC to launch the command pallete and type in "snippets". Select the option `Preferences: Configure User Snippets`and select the language you are setting up the snippets for - in this case CSS. 

Inside of this file, you can paste the following code:

```json
{
	"Border Box": {
		"prefix": "bor-box",
		"body": "* { -moz-box-sizing: border-box; -webkit-box-sizing: border-box; box-sizing: border-box; }",
		"description": "Box Sizing Snippet"
	},

	"Normalize": {
		"prefix": "normalize", 
		"body": [
			"article,aside,details,figcaption,figure,footer,header,hgroup,nav,section,summary{display:block;}audio,canvas,video{display:inline-block;}audio:not([controls]){display:none;height:0;}[hidden]{display:none;}html{font-family:sans-serif;-webkit-text-size-adjust:100%;-ms-text-size-adjust:100%;}a:focus{outline:thin dotted;}a:active,a:hover{outline:0;}h1{font-size:2em;}abbr[title]{border-bottom:1px dotted;}b,strong{font-weight:700;}dfn{font-style:italic;}mark{background:#ff0;color:#000;}code,kbd,pre,samp{font-family:monospace, serif;font-size:1em;}pre{white-space:pre-wrap;word-wrap:break-word;}q{quotes:\\201C \\201D \\2018 \\2019;}small{font-size:80%;}sub,sup{font-size:75%;line-height:0;position:relative;vertical-align:baseline;}sup{top:-.5em;}sub{bottom:-.25em;}img{border:0;}svg:not(:root){overflow:hidden;}fieldset{border:1px solid silver;margin:0 2px;padding:.35em .625em .75em;}button,input,select,textarea{font-family:inherit;font-size:100%;margin:0;}button,input{line-height:normal;}button,html input[type=button],/* 1 */input[type=reset],input[type=submit]{-webkit-appearance:button;cursor:pointer;}button[disabled],input[disabled]{cursor:default;}input[type=checkbox],input[type=radio]{box-sizing:border-box;padding:0;}input[type=search]{-webkit-appearance:textfield;-moz-box-sizing:content-box;-webkit-box-sizing:content-box;box-sizing:content-box;}input[type=search]::-webkit-search-cancel-button,input[type=search]::-webkit-search-decoration{-webkit-appearance:none;}textarea{overflow:auto;vertical-align:top;}table{border-collapse:collapse;border-spacing:0;}body,figure{margin:0;}legend,button::-moz-focus-inner,input::-moz-focus-inner{border:0;padding:0;}"
		],
		"description": "CSS Reset Snippet"
	},

	"Clearfix": {
		"prefix": "clearfix",
		"body": " .clearfix:after {visibility: hidden; display: block; font-size: 0; content:''; clear: both; height: 0; } ",
		"description":"Clearfix Snippet" 
	},
	
	"Setup": {
	"prefix": "setup",
	"body": [
		"article,aside,details,figcaption,figure,footer,header,hgroup,nav,section,summary{display:block;}audio,canvas,video{display:inline-block;}audio:not([controls]){display:none;height:0;}[hidden]{display:none;}html{font-family:sans-serif;-webkit-text-size-adjust:100%;-ms-text-size-adjust:100%;}a:focus{outline:thin dotted;}a:active,a:hover{outline:0;}h1{font-size:2em;}abbr[title]{border-bottom:1px dotted;}b,strong{font-weight:700;}dfn{font-style:italic;}mark{background:#ff0;color:#000;}code,kbd,pre,samp{font-family:monospace, serif;font-size:1em;}pre{white-space:pre-wrap;word-wrap:break-word;}q{quotes:\\201C \\201D \\2018 \\2019;}small{font-size:80%;}sub,sup{font-size:75%;line-height:0;position:relative;vertical-align:baseline;}sup{top:-.5em;}sub{bottom:-.25em;}img{border:0;}svg:not(:root){overflow:hidden;}fieldset{border:1px solid silver;margin:0 2px;padding:.35em .625em .75em;}button,input,select,textarea{font-family:inherit;font-size:100%;margin:0;}button,input{line-height:normal;}button,html input[type=button],/* 1 */input[type=reset],input[type=submit]{-webkit-appearance:button;cursor:pointer;}button[disabled],input[disabled]{cursor:default;}input[type=checkbox],input[type=radio]{box-sizing:border-box;padding:0;}input[type=search]{-webkit-appearance:textfield;-moz-box-sizing:content-box;-webkit-box-sizing:content-box;box-sizing:content-box;}input[type=search]::-webkit-search-cancel-button,input[type=search]::-webkit-search-decoration{-webkit-appearance:none;}textarea{overflow:auto;vertical-align:top;}table{border-collapse:collapse;border-spacing:0;}body,figure{margin:0;}legend,button::-moz-focus-inner,input::-moz-focus-inner{border:0;padding:0;}",
		"",
		".clearfix:after {visibility: hidden; display: block; font-size: 0; content: ''; clear: both; height: 0; }",
		"",
		"* { -moz-box-sizing: border-box; -webkit-box-sizing: border-box; box-sizing: border-box; }"
	],
	"description": "Normalize, Border-Box, Clearfix"
	},

	"VisuallyHidden": {
		"prefix": "vhidden",
		"body": ".visuallyhidden:not(:focus):not(:active) { position: absolute; width: 1px; height: 1px; margin: -1px;border: 0;padding: 0;white-space: nowrap;clip-path: inset(100%);clip: rect(00 0 0);overflow: hidden;}",
		"description": "Visually Hidden Snippet"
	}
}
```
Repeat the above steps for SCSS.

We should now have access to the following snippets in CSS/SCSS: 

* `bor-box` + `tab`
* `normalize` + `tab`
* `clearfix` + `tab`
* `setup` + `tab`

And the following snippets in HTML: 

* `jquery` + `tab`
* `responsive` + `tab`

Don't stop here - feel free to make your own! 