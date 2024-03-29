# GitHub Demo Instructions

*add link for SSH key install

Hi all!  For the interactive lab today, please do the following:

* Have a question?  Put it as an issue.  We might want to add it to the documentation in an FAQ section or expand it to be it's own section too!
* Note any issues you see with spelling, grammar, or general information you feel needs presented differently.  Put it as an issue, as we are going to fix it during the demo today to get some hands-on practice using git.

### Need to install git?

Go here: <https://github.com/git-guides/install-git>

### Getting Started with git

To contribute to a project, the first thing you want to do is clone the projecct.  This creates a local copy that you can work from, keep history of code changes, and ultimately merge your changes with collaborators. To do this the command you use is *git clone*.  To clone a repository, you first need to find the respository name, which can be found here:

![repo screenshot](images/repo_name.png)

Note you can use multiple methods to authenticate, and the url is different for each one.  Once you know the repository name, you would type the following command into your terminal:

```
git clone 'repository name'
```

If that wasn't successful, and you received an error, refer to this

help page <https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository>.

### Writing code in git

Before you make any changes to any files, you first need to create your own branch.  This repository has a few branches that are *protected*, or branches that you can't directly make changes on.  These branches, the *master* and *test-pypi* branches can be configured to integrate directly with pypi for package distribution, and as such, require approval and code review to merge any changes.  Each branch should correspond to a software feature or issue with the code, and be named accordingly.  For example, for the creation of this readme file, we can create a branch called *readme*, and then make changes on that branch.  To do so navigate to the main repository folder in terminal and type:

```[bash]
git branch readme
git switch readme
```

Any changes you make should now be saved in the branch named *readme*.  If you aren't sure what branch you are on you can always check:

```[bash]
git branch
```

It's important to note that when creating new branches, they make a copy of the branch you are currently on.  So if you are on *master* and create a new branch, it will be a copy of *master*.  In the section below on structuring releases in git we will review a recommended workflow.

You can learn git commands on Git branching here: [Git branching Interactive tool](https://learngitbranching.js.org/)

### Committing and pushing changes in git

Once you've made progress you'd like to save on a branch, you need to *commit* your changes, which saves them to the branch and allows you to save them on the repository on the GitHub servers for other people to access, review, and approve merges.  To see what changes are available to be committed, you can check the status:

```[bash]
git status
```

which will show something like:

![git status](images/git_status.png)

Anything under *Changes not staged for commit* will save when you commit your changes.  Anything in *Untracked files* needs to be added for commit, or listed in the .gitignore file.  For now, assume this is a file or folder we do want to save in our changes, and we will discuss .gitignore later in the document.  To add the file, you use the *git add* command, and to add all files and folder that are untracked you would type:

```[bash]
git add .
```

You can then check the status again:

```[bash]
git status
```

and get the following output:

![git status new](images/git_status_new.png)

To commit your changes:

```[bash]
git commit -m 'status message'
```

The status message should describe the changes you made in some detail so someone reviewing your code would understand the intention of this code.  Once you've committed the changes, you can push them to the GitHub server:

```[bash]
git push origin readme
```

The *origin readme* says to push to the GitHub server to a branch named readme.  To configure the GitHub server readme branch to correspond with your local readme branch to be able to just run *git push* do the following:

```[bash]
git push --set-upstream origin readme
```

Now any changes you need to push to the github server on the readme branch can be done by just running:

```[bash]
git push
```

### Structuring and merging code in git

When working on a project in git, it's a good idea to organize the features you want to include into groupings of functionality that make sense to be included together, called *releases*.  For each feature you create a branch, and then these branches are merged together on another branch for the release.  So for example, if I have three branches that are all basic features of a package that I want to include in the same release, I'll first create a release branch and merge these onto the release branch.  Here we introduce a new command that creates and switches to the new branch at the same time.

```[bash]
git switch -c version-0.1
```

And we can see we've created and switched to the new branch named *version-0.1*

![git switch c](images/git_switch_c.png)

We also see we already have a readme branch, so let's create some new branches.  We can do this in the terminal, but since we are going to tie them to releases, we will actually show how to create them in the GitHub web interface.  First, I'm going to commit and push all changes to make sure it is up to date between the local branches and the remote branches.

I'll navigate to the repo here: <https://github.com/barnesd8/github_template> and go to the issues area.

![git issues](images/git_issues.png)

I'll then drill into the highlighted one here:

![git status message](images/git_status_message.png)

And then click *Create a branch*:

![git create branch](images/git_create_branch.png)

You can also change which branch you are copying from by choosing *change branch source*:

![git change source](images/change_branch_source.png)

I am going to choose to create the branch from the *version-0.1* branch:

![git version branch](images/git_version_branch.png)

This is then displayed to copy and paste and get the version locally to start working on the issue:

And then this is shown when it is run in the terminal:

You've now created a new branch to work on your issue!

### Merging code

There are a few ways to merge code, and I recommend using github.com to request merges, request code reviews, merge code, and resolve merge conflicts.  To get started, we need to understand a *merge*, which means we are combining the code from two different branches to be one branch.  Most of the time this is simple, but sometimes a manual review is required to fix *merge conflicts*, or issues where two sets of code are not able to be merged without manual review.  First let's go through the process for a simple merge.

We first identify the branch we'd like to merge and initiate the merge:

![git simple merge](images/simple_merge_request.png)

We then review the branches that will be merged, and confirm the request:

![git simple merge](images/simple_merge_request_pt2.png)

And:

![git simple merge](images/confirm_simple_merge.png)

And:

![git simple merge](images/confirm_simple_merge_pt2.png)

And because this was connected to an issue, we go head and close it:

![git simple merge](images/close_issue.png)

Our simple merge is now complete, and the issue is closed.  We now need to update our local repository to match the github server.  First we switch to the branch that we merged onto - *in this example is it the version-0.1 branch* - and then pull the changes from the remote repository.

```[bash]
git switch version-0.1
git status
git pull
```

The following is displayed and validates our local branch is now up to date with our remote changes.

![git simple merge](images/git_switch_version.png)

The last thing we need to do, since when we merge branches we have our github repository to automatically delete branches that have been merged onto other branches, is delete that branch locally.  We can do that with the following command:

```[bash]
git branch -d 3-remove-s-from-git-commit-status-message
```

### Merge Conflicts

You won't always be able to automatically merge code - sometimes changes with conflict with each other, so you need to modify code to solve the conflict.  When this is the case, you'll end up at a screen like this:

![git merge conflict](images/merge_conflict_pt0.png)

This means to merge your code, you need to manually review.  And then another to allow you to review the conflicts.

![git merge conflict](images/merge_conflict.png)

Choose the option to resolve the conflicts, and you're looking for an area like the circled one below:

![git merge conflict](images/code_conflict.png)

Make the appropriate updates to your code, save, and you should then be able to merge since the conflict is resolved!

![git merge conflict](images/solved_conflicts.png)

### Merging onto protected branches and code review

The way our projects are configured is with a master branch that is *protected*, which will not allow you to directly commit changes to that branch.  You first need to commit changes to a different branch, and then do a merge request.  Because the branch is protected, a code review will be required before the merge request is approved.  Different projects might have different settings, and they can be modified in the settings tab, under branch protection rules:

![git merge conflict](images/branch_protection.png)

And drilling in gives the following options:

![git merge conflict](images/branch_protection_rules.png)

So to merge onto the master branch, you initiate the merge request as normal.  You will then get this:

![git merge conflict](images/protected_merge.png)

You will need to add a reviewer:

![git merge conflict](images/reviewer.png)

The reviewer will get a notification, and once they've completed their review, you'll get a notification.  You'll be provided feedback like this:

![git merge conflict](images/reviewer_feedback.png)

You can make any corrections in the code either by modifying the original file(s) and committing to the same branch, or in the github user interface.  If you choose to do so in the user interface, make sure you navigate to the correct branch first, and you'll see this when you modify the file:

![git merge conflict](images/reply_to_feedback.png)

If you do update in the interface, it will be a commit like normal and will require a commit message to save:

![git merge conflict](images/commit_from_gui.png)

To complete the code review, you need to resolve any feedback that was provided during the code review:

![git merge conflict](images/resolve_conversation.png)

Once that's done, you'll see the status has been updated, but you still can't merge.

![git merge conflict](images/convos_resolved.png)

Once you reply to and fix any issues as noted in the code review, the reviewer will need to approve the changes and approve the review.  Once this is done, you'll get the following:

![git merge conflict](images/good_to_merge.png)

You can then go through the normal steps to confirm the merge!

### Remember the walnuts

Life is better when you scan tiny brains.

![walnut](images/walnuts_orange_06.png)

### Now you are ready to tackle git

![cat_error](images/cat_error.webp)
