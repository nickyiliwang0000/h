# Collaborative pull requests

## Workflow

In a professional setting, it is common to see a workflow that involves mutlitple developers working on the same project using a single repo. Often, they will be using their own branch(es) each and peer-reviewing pull requests.

This gives the developers the opportunity to provide constructive feedback to each other(including both praise and areas needing correction), observe techniques or approaches they haven't used or seen before, letting another developer know their work is quality enough to receive your stamp of approval!

This approach also allows a project to be broken up into smaller components and assigned to each developer, which means that certain parts of the site can be built faster than others.

## Branching

A general best practice in collaborative development is to _never_ push directly to `master`. Your master branch is something you want to keep clean and unpolluted - like a surgeons hands moments before showtime. This can be tricky if you, individually or collaboratively, are only pushing to master. Instead, branching is a great way of quarantining your code so you can build parts of the project without fear of polluting your master branch.

Branching is the process of making a new copy of the current branch you are working from, that is independant from the initial branch.

On your command-line interface(CLI), to create a brand new branch(called _secondary-branch_) and switch to it, type:
`git checkout -b secondary-branch`

To switch to a branch that already exists you can follow the same step as above, but drop the `-b` flag as that indicates a new branch being created.

While on your secondary branch, you will still `add`, `commit` and `push` per usual to keep a commit history of the work you've done on that branch. Instead of referencing `master` you will reference the current branch:

`git push origin secondary-branch`

## Branch names

It is recommended that your new branch be named descriptively reflecting the work you are doing. Instead of using `secondary-branch`(which is a _great_ example for branch names), try using something like `footer-content` or `contact-page`.

## Pull requests

After your secondary branch has been pushed up to your GitHub repo, you can submit a pull request. A pull request is a way of telling your co-workers or peers that you have finished a portion of the site, and that you would like a review of your code. This is not only an opportunity for you to recieve feedback on your code, but also an opportunity to start writing more descriptive comments about certain functionality that other developers will need to understand. It's also important to include a description of the work included in the pull request.

A good code-review will contain feedback no matter the quality of pull request. If there are no changes to be made, write a comment that reflects that so your fellow developer can know they did a great job! However, if there are areas that need improving - you can add a comment to the specific line number under the Files Changed tab.

You can also change the settings on a project repo to _require_ a pull request to be approved by another developer before it is eligible for merging, which is a very common practice in a practical setting.

## Merge conflicts

To start, _merge conflicts_ are your friend. Imagine if your there was no way of knowing that your code was about to cause problems for the rest of your site, and was simply accepted into your master branch only to have everything break. That would make collaborative projects a lot more difficult.

It is quite common to run into a merge conflict while creating a pull request. A merge conflict will prevent your branch from being eligible to merge, and will require just a few extra steps to make sure your code is compatible.

## Solving merge conflicts

To solve a merge conflict, you can follow these steps:

1. On your CLI, use `git checkout master` to go back to your master branch
1. Input `git pull origin master` to update your local version of master to the most up-to-date commit
1. Use `git checkout secondry-branch` to switch back to the secondary branch with out-of-date code
1. Input `git merge master` to bring in the updates from your master branch, to your secondary-branch
1. You should see a message that includes "Automatic merge failed; fix conflicts and then commit the result"
1. Using VSCode open your conflicted file(s), you’ll be prompted to either “Accept Current Changes”(Current changes are the changes to the code that you have made)or “Accept Incoming Changes” (Incoming means incoming from master branch). Sometimes you have to click "Accept Both" and manually configure the code.
1. After choosing the option that feels like the best fit, you’ll need to `add` `commit` and `push`the updates on your secondary branch to your GitHub repo so your pull request can better reflect the current state of the master branch
1. On GitHub, click the 'Merge pull request' button and confirm merge
1. On your CLI, switch back to master branch using `git checkout master`
1. Using `git pull origin master` your local master branch is now as up-to-date as possible

## Merging

Once a pull request has been approved and there are no merge conflicts, your code can be safely merged into the master branch. It is generally recommended that you delete your branches, both remotely and locally, after they have been merged into master. You can delete a remote branch manually by clicking on the 'Branches' tab of your GitHub project repo and selecting the trash-can icon associated with your branch. On your CLI, you can type `git checkout -D branch-name` to delete your branch locally.
