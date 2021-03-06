<!-- Student takeaway -->
<!-- By the end of this lesson, the student should be able to:
- Add their name + email to git via the command line
- Initialize git on their local machine
- Create a .gitignore file BEFORE their first push to GitHub
- Create a Git repository in GitHub
- Link their GitHub repo to their local repo using git remote add origin
- Describe a Git workflow (make local changes, git add, git commit + message, git push)
-->
# Git on the command line

Download and install [the latest version of Git](http://git-scm.com/downloads) if you haven't already.

## Configuration

When Git takes snapshots of your code, it will associate them with your name and email address. This is useful when collaborating and sharing your work. Open up the command line and type the following commands to confirm that you have set the correct username and email:

```bash
git config --get user.name
git config --get user.email
```

If you need to reset your global username/email configuration, run the following commands:

```bash
git config --global user.name Your Name
git config --global user.email  yourname@your-email.com
```

It should print the name and email address that you set. If there's a typo, reset either one using the same command.

## Initializing a Git repository
Now that everything is all set up, we're ready to **git** started (heh heh).

Let's create a new folder where we will perform all of our git tasks. In the command line `cd` into your desired directory and create a new folder:

```bash
mkdir my-first-git-repo
```

When complete, `cd` into `my-first-git-repo` then run `git init` to initialize a Git _repository_ (often called a _repo_). All a repository does is hold the code you give it. It's like a folder on GitHub's server. This is the first command we will always run when creating a new git project. 

The directory will not visibly change in any way. The `git init` command actually creates a hidden folder called `.git` inside of the directory. If you haven't already configured your computer to show hidden files, do so.
* Mac users can type `Command + Shift + .`.
* Windows users can go to **Explorer > View** and toggle on the **Hidden** checkbox.


## Creating a repository
Before we start adding, committing, and pushing changes to a repository, we need to know which repository we're pushing to. Though it is possible to [create a GitHub repo via the command line by accessing their API](https://developer.github.com/v3/repos/#create), it's much more straightforward to just do it from the website itself.  

1. Log in to [github.com](http://github.com).
2. Follow the instructions for creating a repository here: [https://help.github.com/articles/create-a-repo](https://help.github.com/articles/create-a-repo) but **skip the "Create a README for your repository"** section.
3. From the command line in your git initalized project, add the GitHub repository as a **remote** using the following command:

```bash
git remote add origin https://github.com/<yourusername>/<your-repo-name>.git
```
This line can be copied from the new repo's instructions.

To check if you've done it correctly type this command, which will tell you what your origin and upstream URLs are. 

```bash
git remote -v
```

This step creates a relationship between your local repository and the repository hosted on github.com. [Like Dorian Gray and Basil Hallward's painting of him](https://en.wikipedia.org/wiki/The_Picture_of_Dorian_Gray#Plot), these repos are linked so you can pass information between them and update each from the other. 

If your `git remote -v` tells you that your origin is not what you want it to be, never fear! We can reset the origin. [Detailed directions](https://help.github.com/articles/changing-a-remote-s-url/) can be found on GitHub's website but essentially you will be typing:

```bash
git remote set-url origin https://github.com/<yourusername>/<your-repo-name>.git
```

## Git workflow
When using Git, whether through a GUI or the command line, a strict workflow will keep you from getting confused. Let's go over a Git workflow and some terminology.

### Working directory
The _working directory_ is the folder that contains all your project files. This is where you make changes to your code and add or remove files. It is sometimes called a _local_.

Let's go ahead and create an `index.html` file and add it to our git project:

```bash
touch index.html
```

### Staging area / adding updated files
The _staging area_ is where you collect updated files/folders to eventually be saved as a snapshot or version of your project. Only the files that have been changed need to be staged.

To check if files have been changed, use the `git status` command from the command line inside your working directory. You can use this command at any time to check the status of your files. 
<!-- 
In the GitHub GUI, when any files are changed, they show up in the **changes** tab and stay there until you commit them. -->

If we see some files have changed and we want to keep those changes, we need to **add** these files to the staging area. There are several different ways to add files:

command | what it does
---|---
`git add <file-name>` | Adds/stages a specific file
`git add -A` | Adds/stages all new, modified and deleted files
`git add .` | Adds/stages new and modified, without deleted files
`git add -u` | Adds/stages modified and deleted, without new files

### Commiting your changes
After you add your files to the staging area, you **commit** these changed files to your Git history with a message about what the changes are. (The `-m` flag stands for message).

```bash
git commit -m "added styling for mobile, removed extra files"
```

For your first commit, it's common for your message to be `initial commit`. Otherwise, it is best to keep them to a concise detailing of the changes you've made.

### Pushing your files to GitHub

Up until this step, everything you've done in the command line has happened on your personal computer (a.k.a. locally). Your repository that is hosted online via github.com has not changed yet. (The painting of Dorian Gray is still beautiful.) We need to **push** the code to GitHub so that GitHub looks like our local.

```bash
  git push origin master
```

You may have noticed that we used the word `origin` once before: when we linked your github.com repo with your local one. Think about what we might be doing here. After pushing to master, you should see your changes on github.com.

<!-- We'll go into exactly what `origin` and `master` mean a little later.  -->

> When we're working through this as a class, we may have some trouble pushing to our repositories. Since we're all working from the same IP address, GitHub thinks we might be malicious (40 people trying to do the same thing at the same time 🤔) and temporarily stop us from pushing our code. If you find that you are having trouble pushing to master, wait a few minutes and try again.

## Ignoring things with .gitignore

We don't always want to push every file from our local directory to GitHub. Things like giant PSD files, database information, and production tools (a.k.a. the `node_modules` folder) cause hella conflicts and generally mess up your workflow. In order to tell Git what to ignore when we check `git status`, we can create a `.gitignore` file with the files/folder paths to ignore.

### Example of a .gitignore file

```bash
node_modules
.DS_Store
*.pdf
*.zip
```
This is telling Git to ignore the `node_modules` folder, the hidden file called `.DS_Store` and any files with the extensions `.pdf` or `.zip`.

It's beneficial to create this file **BEFORE** you commit anything, because it will be difficult to ignore files that have already been committed. It is possible to remove the references to these files, but they will exist in the history of the project.

## So, in summary:

**Your Git workflow:**
1. Work (i.e. write code, make changes, add/remove files, etc.)
2. Add files to staging area when you're done a chunk of work. (`git add <file>`)
3. Take a snapshot. (`git commit -m "a useful commit message here"`)
4. `git push origin master` to update github.com repository.
5. Repeat steps 1-4.  

## Exercise

* Navigate to one of your project folders and initialize Git inside of it. 
* Use Github to create a new remote repository and connect it to your local git project
* Create a `.gitignore` file to ignore some of the files in your project. (e.g. `.DS_Store`)
* Add all of the files in your working directory to the staging area.
* Take a snapshot by committing with the message "initial commit".

**Pro-tip: commit early and commit often**

It's tempting to wait until you're "done" to make a commit but it's better to commit early and often. Commit every time you've completed a small chunk of code, a feature, or at the end of the day. The more often you commit, the more "snapshots" and backup copies you'll have to roll back to if you've really messed up your code!  

When you are actively working on a project, try to commit at **least** at the end of the day (though it'll probably be more likely that you'll commit several times a day). Even if you're not done with a feature, your commit message could just be "saving work".  

## Resources

* [Git cheatsheet](https://help.github.com/articles/git-cheatsheet)!
* [GitHub's docs](https://help.github.com/categories/managing-files-in-a-repository/) are helpful and well-written. 
* [Another version of what we did today](https://readwrite.com/2013/10/02/github-for-beginners-part-2/).