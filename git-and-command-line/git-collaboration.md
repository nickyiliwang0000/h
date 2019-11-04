  <!-- Student takeaway -->
  <!-- By the end of this lesson, the student should know:
  - How to create a branch
  - How to switch between branches
  - How to merge a branch
  - How to delete a branch
  -->

# Git collaboration 

Download [these starter files](https://hychalknotes.s3.amazonaws.com/git-branching-lesson.zip) and initialize git in the root directory with the `git init` command. Then, go to GitHub and create a new repository. Add that repo's URL as the origin with `git remote add origin <url>` and commit your starter files.

## Branching
When you're working with files on GitHub, you may want to keep a separate, clean copy locally and tinker with some new features or test out some wild ideas. Great! You're ready to make a git _branch_!

Every new git repository starts with an initial default branch that git automatically names the `master` branch.

In our terminal, we can always determine which branch we are on by running the `git branch` command. An asterisk beside a branch name will indicate it is the current one.

## Example branch workflow setup

Branches are copies of a repository's files. They're a safe place to mess around with the code for your project without:
  1. creating a new git repo for the same project
  2. breaking code or damaging any files in your project

This diagram represents a sample git workflow for a repo: 

![git branching diagram](http://cl.ly/image/3a3M3U2S0v3X/gitbranches.png)

The `master` branch is the _production_ branch (a.k.a. the official finished and stable version of the repo, and probably the one that is live on the internet).

The `feature` branches are where individual developers are writing code and figuring out new features or updates for the website.

(Sometimes a larger company will have a `test` branch where the dev team is trying out new features and seeing how they mesh with the `master` code **without** messing up the live site. We'll only be working with `master` branches and `feature` branches.)

## Create a new branch

We are at a point in our project where we want to start adding new features but want to do so in a safe environment. The `master` branch cannot be our testing ground.

`git checkout -b myFeatureBranch` creates a new trackable branch called `myFeatureBranch` using the `master` branch as a base. The `git checkout -b` part of this command tells git to both create a new branch _and_ switch over to the new branch we created, `myFeatureBranch`.

If we run the `git branch` command now we will see our current branch will be `myFeatureBranch` and not `master`.

This is where you'll write the code that creates a feature for your website. Let's toss an `h1` in `index.html`.

Going forward, the names of your branches should logically reflect the type of work being done. For example, a task to implement a site footer could be completed on a branch called `add-site-footer`. A branch name should help distinguish it from any other.

## When you're ready to commit your changes

Add, commit, and push the change we made to the `myFeatureBranch` branch on GitHub:

```bash
git add -A
git commit -m "adding an h1"
git push origin myFeatureBranch
```

## Switching branches

Use the `git branch` command to confirm which branch you're on but also to see a list of all created branches for your project. If we want to switch to a different branch, we use the `git checkout <branchName>` command.

If you're in your `myFeatureBranch`, use `git checkout master` to switch to your `master` branch.


## Merge a feature branch into master

Once the work on your feature branch has been completed, it is time to update the `master` branch with those changes.

1. Use `git pull origin master` to make sure your local branch is up to date with the latest from the upstream `master`. 
2. Use `git merge myFeatureBranch` to merge your feature branch into the `master` branch.
3. Use `git push origin master` to push your merge to the master branch of your repo on GitHub.

## Stashing changes

If you need to switch to another branch before you're ready to commit your changes, `git stash` will put away the current changes on your branch for later so you can go do stuff in another branch without having to commit these changes.

When you are ready to reapply the code you have stashed earlier, `git stash apply` will bring it back.

## (Optional) Delete the feature branch if you don't need to come back to it
If you're in your feature branch, use `git checkout master` to go somewhere that's not the branch you want to delete.
Use `git push origin :myFeatureBranch`  to delete the `myFeatureBranch` branch on GitHub (upstream). 
`git branch -d myFeatureBranch` will delete the local branch on your computer.

## Resources

Here's a little gif about branching:
![gif about branching](https://hychalknotes.s3.amazonaws.com/git-branching-demo.gif) 
