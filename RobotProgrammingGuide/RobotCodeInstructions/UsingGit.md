# Using Git

## A normal end-to-end git workflow

When working with branches, you will typically follow a workflow like below:

1. Switch to the master branch. Run `git checkout master`. This will fail if you have pending changes. If you don’t have any pending changes you care about, you can run `git clean -d -f`. If that doesn’t solve the problem, run `git stash`. If you have changes you care about from a previous topic branch, see step 5 and come back here after step 7 or 8. If you started making changes before following these steps, see [So you started coding before creating a topic branch](#so-you-started-coding-before-creating-a-topic-branch) below.
2. Get the latest changes that exist on the server onto your local machine. Run `git pull`.
3. Create and switch to a topic branch for your change. Your topic branch should have a name based on what you’re working on. Run `git checkout -b topicbranchname` (don’t forget to replace `topicbranchname`!).
4. Make changes to your code.
5. Commit all of your changes to your local topic branch. Run `git commit -a -m "description of my change"`.
6. Repeat steps 4 and 5 as necessary.
7. Share your changes with the world. Run `git push`. You will probably get a message saying that your topic branch isn’t being tracked upstream. You can either copy and paste the message it gives you, or run something like `git push --set-upstream origin topicbranchname` (don’t forget to replace `topicbranchname`!).
8. Go to [https://www.github.com/irs1318dev], navigate to the repository you are working in, and create a pull request to merge your changes into master. If you can’t figure that out, ask a mentor.

## So you started coding before creating a topic branch

If you started coding in "the wrong branch," you can usually recover as long as you don’t have changes from another topic branch mixed in. You can do something like:

1. Stash your changes. Run `git stash`.
2. Switch to the master branch. Run `git checkout master`.
3. Get the latest changes that exist on the server onto your local machine. Run `git pull`.
4. Create and switch to a topic branch for your change. Your topic branch should have a name based on what you’re working on. Run `git checkout -b topicbranchname` (don’t forget to replace `topicbranchname`!).
5. Retrieve your changes from the stash. Run `git stash pop`.
6. Continue making changes to your code. Follow steps 5–8 in the section above ([A normal end-to-end git workflow](#a-normal-end-to-end-git-workflow)).
