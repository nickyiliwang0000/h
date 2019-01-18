# Keeping organized as a developer

## Naming files and project folders 

As a developer, you will be required to manage many projects, and within those projects, there will be many files and folders. A lot of those files and folders will have the same name. Maintaining an organized file system is **crucial** to ensuring that project assets are kept together and it's easy to access what you need.

### No spaces!

Now that you're a developer, you're going to take the spaces out of your folder names. Spaces can cause a bunch of frustrating issues down the line, so get into the habit of removing spaces from your folder and files names now.

**👎 INCORRECT**
```bash
- project one
  - home page.html
-project two
  - about page.html
```

**👍 CORRECT**
```bash
- projectOne
  - index.html
-projectTwo
  - about.html
```
Without spaces, filenames can be become harder to read. How do we keep legibility in our no-space file names? Naming conventions!

### Naming conventions

_Camel case_ is a pattern where spaces are removed from strings of text and each word but the first starts with a capital letter.

before camel case| after camel case
---|---
`about page.html` | `aboutPage.html`
`project two` | `projectTwo`

_Kebab case_ is a pattern where the spaces are in strings of text are replaced with hyphens.

before kebab case| after kebab case
---|---
`about page.html` | `about-page.html`
`project two` | `project-two`

_Underscore case_ is a pattern where the spaces are in strings of text are replaced with underscores.

before underscore case| after underscore case
---|---
`about page.html` | `about_page.html`
`project two` | `project_two`

Some people consider underscore a type of kebab case. It really doesn't matter what you use as long as you are **consistent**. When you work with other developers, it's very important to make sure you're on the same page.

There's also a convention called _BEM_, which stands for block-element-modifier. People have verrrry strong opinions about BEM and it's implemented differently in different workplaces, so feel free to [check it out](https://github.com/HackerYou/bootcamp-notes/blob/master/css/X-css-organization-with-bem.md) and try it on one of your projects.

## Development workspace
Working with files all over your computer can get messy quickly, especially because you'll have multiple files named `index.html` and folders named `styles` or `scripts`. There should only be one `index.html` for any given project.

Often, developers create a `sites` or `websites` folder at root of their computer that contains folders for categories of projects. These project folders may include a numbering system that represents project IDs or dates.

**👍 CORRECT**
```bash
- websites
    - client-projects
      - 2018-coca-cola-microsite
      - 2018-rolling-stone-microsite
        index.html
        - styles
        - images
      - 2017-b-baker-blog-redesign
        index.html
        - styles
        - assets
    - personal-projects
        - hacker-you
            - bootcamp
            - week-1
            # ...
        - portfolio
            index.html
            style.css
            - assets
```

**👍 ALSO CORRECT**
```bash
- sites
    - work
      - voyagerWebApp_voyager_201809
      - twitterBot_prestoneAgency_201801
        index.html
        - style
        - assets
      - bloggo_briannaBakerInc_201807
        index.html
        - style
        - assets
    - fun
        - hackerYou
            - bootcamp
            - weekOne
            # ...
        - portfolioSite
            index.html
            style.css
            - images
```

Organize in a way that **makes sense to you** and **can scale** when you start having lots of folders and files.

Putting the folder at the root of your computer will allow for easy access of projects when you use tools like [the command line](https://github.com/HackerYou/no-repeat-bootcamp-notes-2018/blob/master/8.1-command-line.md).

On a Mac, you can access your root directory by opening a new Finder window and clicking your username in the sidebar. You may have a `sites` folder already present, but if not, right-click and create a new folder called `sites` or `websites`.

On Windows, open up Windows Explorer to `My Documents` and create a `sites` or `websites` folder.

## Make a well-named folder now!
During your time at HackerYou, you will be given many exercises and will create many projects.

Within your `sites` or `websites` folder, create a new folder called `hackeryou`. Within that new folder, create a folder for each week of the bootcamp.

```bash
- websites 
# (or sites)
  - hackeryou
    - week1
    - week2
    - week3
    - week4
    - week5
    - week6
    - week7
    - week8
    - week9
```

When working on a project, open the entire project folder in your text editor. This should help you stay clear on which file belongs to which project. 

# Close your files when you are not working on them
Also, **close your files when you are not working on them**. Practice tab minimalism. 