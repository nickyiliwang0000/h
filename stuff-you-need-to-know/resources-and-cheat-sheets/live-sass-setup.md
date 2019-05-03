`vscode-live-sass-compiler` is an extension made by a developer with the handle [ritwickdey](https://github.com/ritwickdey/vscode-live-sass-compiler). 

Step by step instructions:
To use this exentsion, 

1. Open the 'Extensions Marketplace'.
2. Type 'Live sass' into the search box.
3. Choose 'Live Sass Compiler' and install.

We'll assume your project folder looks like this:

```bash
projectFolder
  index.html
```

4. Create a folder called `.vscode` inside your `projectFolder`:

```bash
projectFolder
  index.html
  - .vscode
```
5. Create a file inside `.vscode` called `settings.json`

```bash
projectFolder
  index.html
  - .vscode
    settings.json
```

6. Paste this configuration object into `settings.json`:

```json
{
  "liveSassCompile.settings.formats": [
    {
      "format": "expanded",
      "extensionName": ".css",
      "savePath": "./styles"
    }
  ],
  "liveSassCompile.settings.excludeList": [
    "**/node_modules/**",
    ".vscode/**"
  ],
  "liveSassCompile.settings.generateMap": false,
  "liveSassCompile.settings.autoprefix": [
    "> 1%",
    "last 2 versions"
  ]
}
```
7. Save `settings.json`.

8. Create a folder called `styles` with a `sass` folder inside of it.

```bash
projectFolder
  index.html
  - styles
    - sass
  - .vscode
    settings.json
```

9. Create a `style.scss` file:

```bash
projectFolder
  index.html
  - styles
    - sass
    style.scss
  - .vscode
    settings.json
```

10. Start the extension's 'Live Sass: Watch Sass' function by opening the command palette and searching 'Live Sass'.
  * Command + shift + P for Mac
  * Control + shift + P for PC

11. This should create a `style.css` file inside the `styles` folder.
  * If it doesn't, check to make sure your folder organization and save all your files.

12. Create some partials inside the `sass` folder.

```bash
projectFolder
  index.html
  - styles
    - partials
      _header.scss
      _footer.scss
      _setup.scss
      style.scss
  - .vscode
    settings.json
```

13. Import your partials into `style.scss`:
```scss
// inside style.scss
@import 'setup';
@import 'header';
@import 'footer'
```

Now, you should see your styles from your partials showing up in the `style.css` file. 




