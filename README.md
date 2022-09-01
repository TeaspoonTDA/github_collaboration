# github_template
template for GitHub Python projects for the Munch Lab

### Getting Started with git

To contribute to a project, the first thing you want to do is clone the projecct.  This creates a local copy that you can work from, keep history of code changes, and ultimately merge your changes with collaborators. To do this the command you use is *git clone*.  To clone a repository, you first need to find the respository name, which can be found here:

![repo screenshot](images/repo_name.png)

Note you can use multiple methods to authenticate, and the url is different for each one.  Once you know the repository name, you would type the following command into your terminal:

```
git clone 'repository name'
```

If that wasn't successful, and you received an error, refer to this github help page https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository.

### Writing code in git

Before you make any changes to any files, you first need to create your own branch.  This repository has a few branches that are *protected*, or branches that you can't directly make changes on.  These branches, the *master* and *test-pypi* branches can be configured to integrate directly with pypi for package distribution, and as such, require approval and code review to merge any changes.  Each branch should correspond to a software feature or issue with the code, and be named accordingly.  For example, for the creation of this readme file, we can create a branch called *readme*, and then make changes on that branch.  To do so navigate to the main repository folder in terminal and type:

```
git branch readme
git switch readme
```

Any changes you make should now be saved in the branch named *readme*.  If you aren't sure what branch you are on you can always check:

```
git branch
```

### Committing and pushing changes in git

Once you've made progess you'd like to save on a branch, you need to *commit* your changes, which saves them to the branch and allows you to save them on the repository on the github servers for other people to access, review, and approve merges.  To see what changes are available to be committed, you can check the status:

```
git status
```

which will show something like:



### Structuring and merging code in git

When working on a project in git, it's a good idea to organize the features you want to include into groupings of functionality that make sense to be included together, called *releases*.  For each feature you create a branch, and then these branches are merged together on another branch for the release.  So for example, if I have three branches that are all basic features of a package that I want to include in the same release