# Code review best practices

## What is a code review?

When a developer on a team finishes work on an issue, a component, or a project, another developer - or team of developers - will look over the code in order to offer feedback on how the code could be better. Code reviews are an industry-wide practice. All developers will have their code subject to review at some point in their career, if not consistently throughout. Code reviews are classless, meaning that even senior developers will undergo review by all of their peers, including those who are more junior. You can think of it like marking and studying a paper at the same time!


## Why do we code reviews?

Code reviews are not just about offering feedback on someone else's work, but are also a chance to learn from it. Code reviews provide an opportunity to share knowledge!

In a workplace, code reviews will give developers a chance to get to know sections of a code-base that they themselves might not otherwise see. This helps everyone in a company get to know the greater codebase, and share knowledge of the larger scope of a project throughout the team.

Code reviews can also give more junior developers a chance to read more senior developers' code in order to learn from it. Code reviews can act as a way to encourage collaboration and mentorship across teams and individuals.

At this point in your career, practicing code reviews will also help you learn to articulate what you know about coding. You know so much already - Let's talk about it! This is a vital skill in showing others what you know, particularly in job interviews!


## How do we accomplish a great code review?

When you start a review of someone else's code, there is a lot to take in! It is important to approach a code review much like you would with your own code. Start by taking in an overview of the app.

- What is the intention of the app?
- Is it clear to the user what they are to do?
- Does the app interact with the user in predictable ways?

Take your time reading the code. After gaining an overview of the app, take the code in line by line and try to get a cursory understanding of how the developer is accomplishing the functionality of the app. Things to look for in the initial stages of a review include:

- Is the code well organized?
- Is the code DRY?
- Is the code readable and easy to understand. **Good code should be [self-documenting](https://www.sitepoint.com/self-documenting-javascript/)**.


## What specific things should we look for in a code review?

Once you start to get a good understanding of the code being reviewed, it's time to get into the nitty gritty. Generally speaking, try to hold your fellow developer accountable to the highest standards of best practices that you can. **Strict code reviews make better developers!** Some specific things to look for include:

- Is the app and all of its elements accessible? Is dynamically added content accessible?
- Are errors handled effectively? If not, how could they be better handled?
- Are naming conventions followed consistently throughout?
- What is great about the code? It's important to include positive feedback too, so the developer can feel good about the things they've done well!