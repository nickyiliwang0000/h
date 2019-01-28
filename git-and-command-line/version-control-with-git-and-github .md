#Version control with Git and Github

Version control allows us to keep a record of any changes in our directories and files (e.g. updates to the contents of the files as well as adding, removing and renaming files). Version control keeps track of changes without overwriting any part of the project.

You may have been in a situation where you've created an `index-version1.html` and `index-version2.html` or something similar in an effort to preserve a "good" copy while experimenting with another copy.  Version control allows us to save different versions of our entire project, compare them, and revert back to a previous version if needed.  It's also great for sharing and collaboration.

**Git** is type of version control system. It's not the only one! There are many others; another popular one is called **SVN**. The concepts we will learn with Git can be be applied to any version control system.

With Git we can:

* take snapshots (which are called *commits*) of our project folder whenever we want (every type of file is saved, it doesn't have to be code)
* "time travel" between commits
* have different people edit the same file at the same time
* easily share and collaborate on code with others by using services like [GitHub.com](http://github.com)

### Getting Started
To get started, we'll be using [GitHub.com](http://github.com) to host our version controlled projects. This will save our project files on the web and allow us to easily share our code and collaborate with others. Go ahead and sign up for an account if you don't already have one. Your github profile will be linked on your portfolio, resume, and the HackerYou website, so make sure your username is something that you're comfortable being associated with your professional life. 

There are two ways to access Git: using a *GUI* (graphical user interface) or via the command line. We'll be using git with the command line for this course, because it's important to be comfortable working with the terminal, but many people enjoy using a GUI. (A popular one is https://www.sourcetreeapp.com/). Feel free to explore these after the bootcamp.

#### What is a repository?

The purpose of Git is to manage and store information about the changes in a set of files. Git stores this information in a *repository*, which is often shortened to *repo*. 

After you create a repository, it is stored in the same folder as the project itself, in a subfolder called **.git**. Note that directories that start with a `.` are hidden by default on your computer.  You may not see this .git directory on your computer but it may show in other places, such as your FTP client. 

To show files like these, Mac users can type `com.apple.finder AppleShowAllFiles YES` in the command line. Windows users go to **Control Panel > Appearance and Personalization**. In **Folder Options**, select the **View** tab. Under **Advanced Settings**, select **Show hidden files, folders, and drives**.

### Cloning a repository
**Cloning** a repo refers to creating a local copy of an existing repository that you may have access to in your github.com account.  

Where do these repositories come from?  Several sources. If you've been added to an organization, you will have access to repos that have been created in the organization's account.  You can also **fork** other public repos and make contributions to them. 

### The golden rule of source control

**Commit Early & Commit Often** is a rule that you should live by. Making Git part of your workflow when working on a team is crucial. Even when working alone, versioning will give you peace of mind because you'll always have a backup! Need more convincing?  Check out some of these articles:

* [What Is Git & Why You Should Use Version Control If You're a Developer](http://www.makeuseof.com/tag/git-version-control-youre-developer/)
* [GitHub For Beginners: Don't Get Scared, Get Started](http://readwrite.com/2013/09/30/understanding-github-a-journey-for-beginners-part-1#awesm=~oCX648ZyjWDjos)
