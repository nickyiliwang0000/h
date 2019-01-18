# For current and former students 
## So you want to edit the bootcamp notes

We're not perfect! We want your help!

1. Clone the notes to your local.
2. Create a branch and name it the lesson you're editing:
  `git checkout -b 6.19-intro-to-firebase`
  `git checkout -b 3.13-emmet`
  `git checkout -b 5.1-intro-to-jquery master`
  * (if you're not already on `master`, add the word `master` after the name of the new branch you're creating so the base is `master` and not from wherever you are right now.)
3. Make your changes. Add, commit (with a message about what's being changed e.g. `fixing typo in deploy section`) and push to `6.19-intro-to-firebase` (or whatever your branch is called).
4. Check that your changes look how they should.
5. Create a pull request and tag an instructor as a reviewer.
6. Add flags for the kind of pull request it is.
7. An instructor will review it and might ask for changes. 
8. When the changes are made, an instructor will merge it into master.
9. DELETE THE BRANCH FROM GITHUB AND YOUR LOCAL.
10. Thank you!

# For instructors

1. Clone the notes to your local.
2. Create a branch and name it the lesson you're editing:
  `git checkout -b 6.19-intro-to-firebase`
  `git checkout -b 3.13-emmet`
  `git checkout -b 5.1-intro-to-jquery master`
  * (if you're not already on `master`, add the word `master` after the name of the new branch you're creating so the base is `master` and not from wherever you are right now.)
3. Make your changes. Add, commit (with a message about what's being changed e.g. `fixing typo in deploy section`) and push to `6.19-intro-to-firebase` (or whatever your branch is called).
4. Check that your changes look how they should.
5. Create a pull request and tag a team member was a reviewer.
6. Add flags for the kind of pull request it is.
7. A team member will review it and might ask for changes. 
8. When the changes are made, a team member merge it into master.
9. DELETE THE BRANCH FROM GITHUB AND YOUR LOCAL.

## So you want to add a lesson
1. Clone the notes to your local.
2. Create a branch on your local prepended by `new-` and the lesson number and name. (e.g. `07-react-and-firebase/new-6.23-something-new-about-firebase`).
  (We don't necessarily teach them in numerical order.)
3. Add, commit, push to `new-6.23-something-new-about-firebase`
4. Check that your changes look how they should.
5. Create a pull request and tag a team member was a reviewer.
6. Fix any errors they ask you to fix.
7. Have a team member merge it into master.
8. DELETE THE BRANCH FROM GITHUB AND YOUR LOCAL.

## So you want to rename a lesson
1. Don't.
2. (Optional) Bring up that you think a lesson should be renamed in the L10.
3. (Optional) Get approval from bootcamp leads to change the name.
4. (Optional) Change the file name on your local and push to GitHub with the old title in the branch name (e.g. `6.1-functional-programming`).
5. (Optional) Talk to the bootcamp operations manager about what they need to do to make the update with the PCC.

This should be a relatively rare occurrence.
<!-- 
## So you want to remove a lesson
1. Identify the lesson we no longer teach (e.g. `6.1-functional-programming`)
2. Prepend the filename with an `X-`
3. Put it in the deadzone.
4. (Optional) Replace it with another lesson with the same number `6.1-advanced-array-methods`

Every bootcamp we will go through and change any file numbers that need changing. This should be infrequent.

flag | meaning
---|---
`new-` | a new lesson
`X-`| a lesson we no longer teach
 -->
