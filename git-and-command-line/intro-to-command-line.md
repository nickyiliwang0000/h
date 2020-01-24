<!-- Student takeaway -->
<!-- By the end of this lesson, the student should know:
- Various common console commands
-->
# Intro to command line

As developers, we write in many different languages and have lots of exciting tools at our disposal. One of the most powerful tools in our arsenal is tucked away inside the system folder on our computer. It's the low-level interface of our computers which we call the _command line_, and it can greatly improve our workflow.

## Why should a front end developer learn to use the command line?

Front end developers in particular and computer users in general often use visual tools (sometimes called a _graphical user interface_ or GUI - pronounced "gooey") to perform lower-level programming tasks. This makes plenty of sense; if we need to change the color of a button, it's easier to pick a color from a drop-down than it is to create a CSS file, link it, and write a declaration with a hex code. At the same time though, the actions we can perform are limited due to the design of the tool.

A GUI takes a command from us and tells the computer to it. The command line is us telling our computers to run a command witout the GUI in the middle. If the GUI is the barista and the command is our coffee order, the command line is a way for our to make our coffees ourselves. Writing in the command line gives us full control over our system and unlocks super powers for our projects.

## Opening the command line

To open the command line, we can either use the pre-installed command line tool on Windows and Mac, or we can install our own (which allows for even more control over our computers).

* **For Windows:** Click the 'Start' button, choose 'All Programs', navigate to 'Accessories' and choose the 'Command Prompt' application.
    
    If you need to be an administrator, right click the 'Command Prompt' application and choose 'Run as admin'.
    
    For more control over your command line, we recommend you install [cmder](http://cmder.net/).

  If you have Windows 10 you can also install the [Ubuntu Bash](http://www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10/)

* **For Mac:** Open the 'Applications' folder, navigate to the 'Utilities' directory and open the Terminal application.

    For more control over your command line, we recommend you install [iTerm2](http://iterm2.com/).

### Fun fact corner

The name `bash` is a joke because it's a [shell](https://en.wikipedia.org/wiki/Shell_(computing)) based on an [older shell](https://en.wikipedia.org/wiki/Bourne_shell) written by a person named Stephen Bourne. This **new** shell is a Bo(u)rn(e) Again SHell a.k.a. BASH a.k.a. bash. (This is why memes caught on so fast: low bar for internet humor.)

## Common command line commands

In the examples below words in _italics_ (e.g. <code>cd _some/directory_</code>) 
are required parameters for that command that you will replace with your own 
text depending on what you're trying to accomplish. 

MacOS / Linux | Windows | What it does
:-----------: | :---: | ---
`pwd` | `cd` | prints the working directory (i.e. the folder you are inside)
`ls` | `dir` | lists every file and folder inside your working directory
<code>cd _some/path_</code> | <code>cd _some\path_</code> | changes directory to _some/path_
<code>mkdir _name_</code> | <code>mkdir _name_</code> | makes a new directory called _name_
<code>rmdir _name_</code> | <code>rd _name_</code> | removes (deletes) an **empty** directory called _name_
<code>touch _name_</code> | <code>echo. > _name_ | makes a new empty file called _name_
<code>rm _name_</code> | <code>del _name_</code> | deletes a file called _name_
<code>rm -r _name_</code> | <code>rd /s /q _name_</code> | deletes a directory called _name_ **and everything inside it** 
<code>mv _name_ _newname_</code> | <code>move _name_ _newname_</code> | renames a file or directory called _name_ to _newname_  
<code>mv _some/path/name_ _new/path/name_</code> | <code>moves _some/path/name_ _new/path/name_</code> | move a file or directory located at _some/path/name_ to _new/path/name_  
<code>cp _name_ _newname_</code> | <code>copy _name_ _newname_</code> | copies a file named to _name_ to _newname_
<code>cp -r _some/path/name_ _new/path/name_</code> | <code>copy _some/path/name_ _new/path/name_</code> | copies directory located at _some/path/name_ **and everything inside it** to _new/path/name_
`clear` | `cls` | clears your terminal window
<code>open _name_</code> | <code>start _name_</code> | opens _name_ in it's default program, or if _name_ is a directory in Finder / Explorer

### Some important notes on deleting files from the terminal

Deleting files with `rm` or `del` skips the recycling bin. Be careful when using these commands, as the files are deleted immediately, and there is no easy way to recover them.

Similarly, you may come across resources on the internet which use `rm -rf` when deleting files. The `f` option tells `rm` to "attempt to remove the files without prompting for confirmation." If you have accidentally provided an incorrect path, the command may delete a bunch of files you didn't intend to delete. Again, there is no easy way to recover them, so be mindful and try to use this method sparingly.

## Command parameters and options

Often a command requires additional information to achieve the desired results.

### Options

_Options_, which are sometimes also called _flags_, typically change how a 
command will behave. These options usually start with `-` or `--` for MacOS and Linux, and `/` for Windows.

For example the following command lists a directory in MacOS and Linux:

```bash
ls
```
```
Applications                            Library
Desktop                                 Movies
Documents                               Music
Downloads                               Pictures
Dropbox                                 Projects
```

You can specify the "long format" option by using `-l`:
```bash
ls -l 
```

```
total 104
drwx------@   6 cooluser  staff    192 22 Apr 14:21 Applications
drwx------@  28 cooluser  staff    896 25 Apr 10:24 Desktop
drwx------@ 108 cooluser  staff   3456 25 Apr 15:12 Documents
drwx------+ 104 cooluser  staff   3328 25 Apr 15:01 Downloads
drwx------@  60 cooluser  staff   1920 19 Apr 23:19 Dropbox
drwx------@  71 cooluser  staff   2272 25 Apr 14:26 Library
...
```

### Parameters
_Parameters_ typically provide extra information about what you want a command 
to do. Some commands have _required parameters_ which must be provided after the
command. For example, the move command on MacOS and Linux, `mv`, has two 
required parameters: <code>mv _**source**_ _**destination**_</code>:

```bash
mv assets/style.css assets/styles/style.css
```

Parameters that aren't required are called _optional parameters_, and are often
written in documentation with square brackets in documentation (e.g. 
<code>ls _[path]_</code>). 

If your parameter value contains a space, you will almost always need to wrap 
the parameter in double quotes:

```bash
mkdir "My Awesome Directory"
```

### Help!
When in doubt read the documentation for a command. In MacOS and Linux check to 
see if the command has a _manual page_ by typing `man` followed by the command
you want to learn more about. If a manual page exists you'll be able to browse
the documentation using your arrow keys. Press `q` to quit.

```bash
man ls
``` 
```
NAME
     ls -- list directory contents

SYNOPSIS
     ls [-ABCFGHLOPRSTUW@abcdefghiklmnopqrstuwx1] [file ...]

DESCRIPTION
     For each operand that names a file of a type other than directory, ls displays its name as well as any requested, asso-
```

If there isn't a manual page, or if you're on Windows, often a command will 
provide it's own help summary, usually with the `h` or `help` option and 
on Windows sometimes `?`.

```bash
man -h
curl --help
```
```
dir /?
``` 

## Exercise
If you'd like more practice with the commands from this lesson, follow the directions in this [command line exercise](https://hychalknotes.s3.amazonaws.com/command-line-dolly.md).
