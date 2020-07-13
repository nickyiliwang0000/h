  <!-- Student takeaway -->
  <!-- By the end of this lesson, the student should know:
  - How to make a pull request
  - How to review a pull request
  - How to resolve a change request
  - How to resolve a merge conflict
  - How to merge pull request into main branch
  -->


# Git Collaboration

So far we've learnt about git branching as a way for us to make copies of the project and making changes without messing with the original version of the project. We can then utilize git merge to add and merge our changes into the main version. 

The git branch and git merge workflow is a popular way for multiple developers to work on a project simultaneously. However it's a workflow that is not truly collaborative. A basic git branch and git merge workflow means any developer on the project can merge their work into the original branch at any time, without a review process. This often results in mistakes, or other developers being blindsided by what's been pushed into the main codebase. 

Adding _pull requests_ to our workflow can help us solve that problem. 


## Pull requests

A pull request (also referred to as a _PR_ ) is a way of telling the other devs on a project that you have finished a portion of the site, and that you would like a review of your code. This is not only an opportunity for you to receive feedback on your code, but also an opportunity to start writing more descriptive comments about certain functionality that other developers will need to understand - it's important to have a description of the work included in the pull request.

A good code-review will contain feedback no matter the quality of pull request. If you review a PR and there are no changes to be made, write a comment which reflects that so your fellow developer can know they did a great job! However, if there are areas that need improving, you can add a comment to the specific line number under the 'Files Changed' tab in GitHub.

You can also change the settings on a project repo to require a pull request to be approved by another developer before it is eligible for merging, which is a very common practice in a practical setting.


## Making a pull request

In your repository, create a new branch using the command line `git checkout -b [branch-name]`

Make some changes to your project. 

Go through the git workflow to push your changes:
* `git add -A`
* `git commit -m "[commit message]"`
* `git push origin [branch-name]`

After your branch has been pushed up to your remote repo, go to your GitHub repo page and you should see a notification about your branch: 

<img src="https://hychalknotes.s3.amazonaws.com/create-PR.png" alt="a button allowing a user to create a pull request">

Create a pull request by selecting "Compare & pull request". This will open up the pull request window. Here is where you can provide more information about the content you have changed.  

<img src="https://hychalknotes.s3.amazonaws.com/PR-window.png" alt="create pull request UI" width="700">

After you hit "Create pull request", your PR will be ready for another member on your team to review, comment and provide feedback.


## Reviewing a pull request 

<img src="https://hychalknotes.s3.amazonaws.com/PR-review.png" alt="create pull request UI]" width="500">

GitHub will automatically detect the differences (ie. the changes you made) between the branches your PR is requesting to merge. Another developer can review these changes by clicking on the commit, or going to the "Files changed" tab.

The reviewer can comment on a particular line of code by hovering over the plus icon:

<img src="https://hychalknotes.s3.amazonaws.com/PR-comment.png" alt="pull request comment">

There are 3 actions you can make when reviewing a pull request: 
* **Approve**: This will notify the author that all changes are good, changes are approved to be merged back into original branch
* **Request Changes**: This will notify the author that some changes have to be addressed before continuing. 
* **Comment**: This will just provide general feedback to the author. 

<img src="https://hychalknotes.s3.amazonaws.com/PR-options.png" alt="create pull request UI">

**A note on providing pull request feedback**

Just like giving any other feedback, try to keep your comments and feedback constructive but positive. Comments should be clear and descriptive. 

Bad Feedback 👎
- This code is wrong
- This won't work
- This is really messy

Good Feedback 👍
- Try using `position: relative;` here instead of `margin`, it is more suitable in this situation because we need to break the flow of the page and have the elements overlap.
- This class name is named in kebob-case, we should name it to camelCase to stay consistent with the rest of the site.
- Great work!! (Always remember to recognize good work! With emojis!✨) 

**When a pull request is approved**

If there are no merge conflicts, your code can be safely merged into your main branch. The GitHub UI will provide an option to merge the pull request. Your code will then be successfully merged into the original branch!

<img src="https://hychalknotes.s3.amazonaws.com/PR-approved.png" alt="pull request approved" width="700">

It is generally recommended that you delete your branches, both remotely and locally, after they have been merged. A UI option to do this will appear on GitHub after you've merged. You can also delete a remote branch manually by clicking on the 'Branches' tab of your GitHub project repo and selecting the trash-can icon associated with your branch. On your CLI, you can type `git checkout -D branch-name` to delete your branch locally.

**When a change is requested**

If a reviewer requests a change before approving the PR, you (or whoever the author is) have to address the change locally on your code editor and push up your updates to the branch with `add`, `commit` and `push`. You don't need to create a new pull request, GitHub will know that you've pushed some changes to the same pull request. The review process will be the same. The reviewer can then again either approve or request more changes to be made. This process will be repeated until it is approved!

<img src="https://hychalknotes.s3.amazonaws.com/PR-change-requested.png" alt="pull request change requested" width="700">


## Merge conflicts

_Merge conflicts_ occur when competing changes are being made to the same file.

Merge conflicts are your friend! Imagine if there was no way of knowing that your code was about to cause problems for the rest of your site, and was simply accepted into your master branch only to have everything break. That would make collaborative projects a lot more difficult.

<img src="https://hychalknotes.s3.amazonaws.com/mergeConflict.png" alt="a screenshot from GitHub showing that a branch cannot be automatically merged into master branch">

It is quite common to run into a merge conflict while creating a pull request. A merge conflict will prevent your branch from being eligible to merge, and will require just a few extra steps to make sure your code is compatible.

<img src="https://hychalknotes.s3.amazonaws.com/mergeConflictIndex.png" alt="a screenshot from GitHub displaying the file names that are causing a merge conflict" width="700">

## Solving merge conflicts

To solve a merge conflict, you can follow these steps:

1. On your CLI, use `git checkout master` to go back to your master branch
2. Input `git pull origin master` to update your local version of master to the most up-to-date commit
3. Use `git checkout [your-working-branch]` to switch back to the secondary branch with the out-of-date code
4. Input `git merge master` to bring in the updates from your master branch, to your secondary branch
5. You should see a message that states:
"Automatic merge failed; fix conflicts and then commit the result"
   ![Automatic merge failed message on a command line interface](https://hychalknotes.s3.amazonaws.com/mergeConflictCLI.png)
6. Using VSCode open your conflicted file(s), you’ll be prompted to either 
   - “Accept Current Changes”: Current changes are the changes to the code that you have made 
   or, 
   - “Accept Incoming Changes”: Incoming means incoming from master branch. 
   - Sometimes you have to click "Accept Both" and manually configure the code.
   ![a VScode message allowing the developer to accept incoming changes, accept current changes, accept both, or compare changes](https://hychalknotes.s3.amazonaws.com/acceptChanges.png)
7. After choosing the option that feels like the best fit, you’ll need to `add` `commit` and `push`the updates on your secondary branch to your GitHub repo so your pull request can better reflect the current state of the master branch
8. Once everything looks good, on GitHub, click the "Merge pull request" button and confirm merge
9. On your CLI, switch back to master branch using `git checkout master`
10. Using `git pull origin master` your local master branch is now as up-to-date as possible

