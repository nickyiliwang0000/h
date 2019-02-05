<!-- Student takeaway -->
<!-- By the end of this lesson, the student should know:
- How to host a site in GitHub
- How to merge a gh-pages branch into master
- That rebasing exists
-->

# What is GitHub Pages?

GitHub Pages is a tool you can use to create live sites hosted by GitHub directly from your GitHub repos!

You can make a website for your user account, an organization you belong to, or for an individual project. You get **one** top-level site per GitHub account (or organization) and unlimited project sites. This means that you can have `studentname.github.io` and `studentname.github.io/coolproject` at the same time, but you can't have `studentname.github.io` and `coolproject.github.io`.

## How to create a site from a repo
Let's start with a new site for an individual project. There are two options:

* generate a site with one of the pre-built themes
* create a site from scratch

We're going to do the second one.

1. Head over to github.com and create a new repository including a README file. **If you're using an existing repo, skip to step 5.**

2. Clone the repo to make a local copy. 
  ```bash
    git clone https://github.com/username/repo-name.git
  ```

3. Using the command line, `cd` into the new repo. 
  ```bash
    cd repo-name
  ```

4. Create and switch to a branch called `gh-pages`.
  ```bash
    git checkout -b gh-pages
  ```
  As we've learned, `git checkout` switches between branches, and the `-b` flag creates a new branch at the same time. In our case, `git checkout -b gh-pages` both creates and switches to a new branch called `gh-pages`.

  We should get this message to confirm the switch:
  ```bash
    Switched to a new branch 'gh-pages'
  ```
  (You may get an error message saying you don't have admin privileges, in which case you'll need to type `sudo` at the start of that command.)

5. If this is a new repository, create an `index.html` file (use the `touch` command).
    * If this is an existing repository, make a change to your local copy. 

6. Add, commit, and push the update to the `gh-pages` branch via the command line.
  ```bash
  git push origin gh-pages
  ```
  * If you're using the GitHub GUI, go to the 'Branches' tab and ensure `gh-pages` is selected.

It's that easy! Your site can be viewed at `http://username.github.io/repository-name`. (It might take a few minutes to show up. Go stretch!)

To get our website up and running using [github.com](http://github.com), your files **must be pushed to the `gh-pages` branch**. However, this does not automatically update/sync your master branch. 

> This should make total sense. You made a copy (a branch) of `master` and named it `gh-pages`, then changed some stuff in `gh-pages` and pushed those changes to `gh-pages` on GitHub. So the branch you made the copy from (e.g. `master`) doesn't have the changes you made on `gh-pages`.

At any point, you can run `git status` to check which branch you are currently on if you're using the command line.

### Syncing branches

In the above exercise, we made the changes to the `gh-pages` branch and haven't moved, so we need to switch to `master` to update master. 

> Remember that can use `git status` to check where we are.

So we're going to the branch that we want to **update**. 

```bash
git checkout master
```

To bring the current branch up to date with branch containing the changes, we'll use the `merge` command. Merging will take the changes from `gh-pages` and put them into `master`.

```bash
git merge gh-pages
```

Now we have to `push` these changes to the repository on GitHub.

```bash
git push origin master
```

### Optional: Make `gh-pages` the default branch of a repository
1. In the repository on GitHub, go to the 'Settings' page. 
1. Choose 'Options' in the top section, set the default branch in the dropdown.

![Screencap of settings page](https://hychalknotes.s3.amazonaws.com/changing-default-branch-on-github.png)

## Resources and references

* [GitHub Help](https://help.github.com/)
* [GitHub Pages](https://pages.github.com/)  
* [Get Started With GitHub Pages (Plus Bonus Jekyll)](http://24ways.org/2013/get-started-with-github-pages/)
* You may see commands online suggesting that you rebase instead of merging. [Read up on rebasing here.](http://gitready.com/intermediate/2009/01/31/intro-to-rebase.html)
* [Easily keep gh-pages in sync with master using rebase.](http://lea.verou.me/2011/10/easily-keep-gh-pages-in-sync-with-master/)
  * Rebasing acts very similar to merging when you're the lone person working on a repo. We're preparing you to work on repos with lots of people!




If you'd like to look into build a blog that can be hosted on Github Pages, check out these tools:
* [http://octopress.org/](http://octopress.org/) - Ruby
* [http://jekyllrb.com/](http://jekyllrb.com/) - Ruby
* [http://hexo.io/](http://hexo.io/) - Node.js
