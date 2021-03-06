  <!-- Student takeaway -->
  <!-- By the end of this lesson, the student should know:
  - How to create a branch
  - How to switch between branches
  - How to merge a branch
  - How to delete a branch
  -->


# Git Branching

When you're working with files on GitHub, you may want to keep a clean copy locally and tinker with some new feature or wild idea. Great! You're ready to make a _branch_!

A branch is an isolated copy of your current work. When a branch is created, it is an exact replica of your last **committed** code. When you initialize a new repo with a project, you only have one branch - your `master` branch!

<img src="https://hychalknotes.s3.amazonaws.com/view-branch.png" alt="viewing branches on github">

On your command-line interface(CLI), if you were to create a new branch based off of the `master` branch, you would have an exact replica of your local-copy of your master branch.


## Why do we branch? 

Since branches are copies of a repository's files, they're a safe place to experiment with the code for your project without:

  1. creating a new git repo for the same project
  2. messing up your current working project

In a professional setting, it is common to see a workflow that involves multiple developers working on the same project using a single repo. Often, they will be using their own branch(es).

This approach allows a project to be broken up into smaller tasks and assigned to each developer. It give developers the ability to collaborate on a project together simultaneously without stepping on each other's toes. 

We will be learning how to collaborate with other developers in more depth using _Pull Request_ in another lesson. 


## Branching workflow

This diagram represents a sample git workflow for a repo: 

![git branching diagram](http://cl.ly/image/3a3M3U2S0v3X/gitbranches.png)

The `master` branch is commonly the _production_ branch (a.k.a. the official finished version of the repo, and probably the one that is live on the internet). The `master` branch is something we want to keep clean and unpolluted - like a surgeons hands moments before showtime. This can be tricky if you, individually or collaboratively, are only pushing to master. Instead, branching is a great way of quarantining your code so you can build parts of the project without fear of polluting your master branch.

The `feature` branches are where individual developers are writing code and figuring out new features or updates for the website.

(Sometimes a larger company will have a `test` or `dev` branch where the dev team is trying out new features and seeing how they mesh with the `master` code **without** messing up the live site. We'll only be working with `master` branches and `feature` branches.)

## Setting up a repo
- Download [these starter files](https://hychalknotes.s3.amazonaws.com/git-branching-lesson.zip).
- In your command line, navigate to the directory and initialize git with `git init`. 
- Then, go to GitHub and create a repo. Copy the repo's URL and navigate back to your command line
- Add git origin to your directory with `git remote add origin [url-provided-by-github]`
- `add`, `commit` and `push` your starter files. Then, follow along with the next steps.

## Creating a new feature branch

On the command line, create a new branch by using the command `git checkout -b my-feature-branch master`.

This creates a new trackable branch called `my-feature-branch` using the `master` branch as a base. This is where you'll write the code that creates a feature for your website. Let's toss an `h1` and write some content in the `index.html`.

**A note on branch names**

Just like CSS class names, there are many ways of naming git branches. Each workplace will also have their own naming guidelines. Whichever way you decide to follow, it is recommended to be consistent and descriptive. Instead of naming a branch as `branch-2`, try using something like `feature/header-nav` which is more descriptive about the work you are doing on the branch. 

## Working on a feature branch

When you're on your feature branch, `git pull origin master` will grab the changes from your `master` branch and add them to your feature branch so you can begin work using the most recent code.

## Switching branches 

If you need to switch to another branch before you're ready to commit your changes, `git stash` will put away the current changes on your branch for later so you can go do stuff in another branch (`git checkout another-feature-branch` to take you to `another-feature-branch` if it's already set up) without having to commit these changes.

`git checkout my-feature-branch` will bring you back to your feature branch and `git stash apply` will bring back what you put away on on `my-feature-branch`.

## When you're ready to commit your changes
Back on `my-feature-branch`, `add`, `commit`, and `push` the change we made to the `my-feature-branch` branch on GitHub:

```bash
git add -A
git commit -m "adding an h1"
git push origin my-feature-branch
```

## Merge a feature branch into master

1. Use `git branch` to check which branch you're on.
   * If you're in your `my-feature-branch`, use `git checkout master` to switch to your `master` branch.
2. Use `git pull origin master` to make sure your local is up to date with the latest from the remote `master`. 
3. Use `git merge my-feature-branch` to merge your feature branch into the `master` branch.
4. Use `git push origin master` to push your merge to the master branch of your repo on GitHub.

If you've got merge conflicts, now is a great time to sit down with your teammates and see which changes you want to keep.

### (Optional) Delete the feature branch if you don't need to come back to it
If you're in your feature branch, use `git checkout master` to go somewhere that's not the branch you want to delete.
Use `git push origin :my-feature-branch`  to delete the `my-feature-branch` branch on GitHub (upstream). 
`git branch -d my-feature-branch` will delete the local branch on your computer.

## Resources

Here's a little gif about branching:
![gif about branching](https://hychalknotes.s3.amazonaws.com/git-branching-demo.gif) 
