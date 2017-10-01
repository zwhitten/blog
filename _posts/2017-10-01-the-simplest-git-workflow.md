---
layout: post
title: The Simplest Git Workflow
date: 2017-10-01 5:34:00 -0500
comments: true
tags: git github workflow
---

## Why? 

I love git. It was a breath of fresh air coming from a heavier Version Control System at a previous job. Git makes coding dare I say, fun? 
Git is extremely powerful. For people unfamiliar with Git it can seem daunting or confusing, either because they're coming from another VCS or they've never used a VCS at all (Shouldn't they be teaching _something_ in schools these days?)

Below I'll outline what I think is one of the simplest workflows you can use on your teams or in your own personal development. The goal is to avoid using some of the more advanced git features which can (when used incorrectly) get developers into trouble. 

**Assumptions:**
- You have git installed and configured
- There is a remote repository of some kind you want to work with
- Your team doesn't already have a policy in place about doing things like rebasing before merging into master, etc.

## Optional Setup
If you don't already have a remote repository setup with write access, you can easily fork an existing repository on github. 

1. Go to the github page for a project you'd like to contribute to, ex: [github/gitignore](https://github.com/github/gitignore)
2. In the top right corner click the `fork` button. This creates a copy of the repository under your account that you will have full read/write access to. 
3. On your own repository page click the `Clone or Download` button to get the repository URL for use in the cloning step below.

## Getting Started

Great you're still here! We'll first want to pull down a git repository. As an example we'll use github's repo with a collection of gitignore files by language type. (If you created a fork in the optional setup replace the git URL below with the URL to your personal repository)

```shell
git clone https://github.com/zwhitten/gitignore.git
```

Which should result in something like this:

```shell
 % git clone https://github.com/zwhitten/gitignore.git
Cloning into 'gitignore'...
remote: Counting objects: 6896, done.
remote: Compressing objects: 100% (14/14), done.
remote: Total 6896 (delta 6), reused 11 (delta 2), pack-reused 6880
Receiving objects: 100% (6896/6896), 1.37 MiB | 1.67 MiB/s, done.
Resolving deltas: 100% (3686/3686), done.
Checking connectivity... done.
```

This will create a directory on your local machine called "gitignore". The rest of the commands will be run from inside this directory so go ahead and go into it

```shell
 % cd gitignore
```

## Working on changes locally

By default git will be on the `master` branch when you first open up the project. Once you know the bug or feature you will be working on, you will want to create a feature branch to do this work. Different teams have different conventions for how they like to name their branches. Some like to prefix their feature branches with "feature/" others don't. For our simple scenario since we won't actually be pushing our feature branch remotely it won't matter _too_ much. 
The gitignore project I checked out contains .gitignore files which can be used in various project types to tell git to ignore specific files or directories. Maybe your team likes to use (but not check in) a series of files ending in ".xyz" in their Java projects and you think the entire github community could benefit from doing the same.

### Create a local branch

- First we'll create a feature branch for this change called `ignore_xyz`:
```shell
 % git checkout -b ignore_xyz
Switched to a new branch 'ignore_xyz'
```
OR 
```shell
 % git branch ignore_xyz
 % git checkout ignore_xyz
Switched to branch 'ignore_xyz'
```
The first option is a shortcut that does the same thing as the second option: Creates the new branch with the specified name and then switches to it. 

### Make your changes

- Now that we're on the feature branch we just created we can make our changes to the Java.gitignore file in the directory by adding "*.xyz" to the top of the file. 
Git allows us to see what changes have been made on our branch by running:

```shell
 % git status
On branch ignore_xyz
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   Java.gitignore

no changes added to commit (use "git add" and/or "git commit -a")
```
This is telling us that we've modified one file on our branch and even gives us hints about how to revert it or move forward with the change. 

- We next add our changed file to the staging area which is git's way of collecting changes to be put into a commit:

```shell
 % git add Java.gitignore
 % git status
On branch ignore_xyz
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   Java.gitignore
```
Our change is now staged and ready to be committed to our feature branch.

- Commits require a message to be added. It's a good idea (and helpful to anyone reviewing your change) to include a useful message that describes what your commit contains:

```shell
 % git commit -m "Adding xyz to Java.gitignore file"
[ignore_xyz 8eafff2] Adding xyz to Java.gitignore file
 1 file changed, 1 insertion(+)

 % git status
On branch ignore_xyz
nothing to commit, working tree clean
```
Great! We successfully committed our change, but currently it only exists in our local feature branch. We'll want to merge this into the master branch to share with everyone else. 

### Switch back to `master`
- We'll switch back over to the master branch using the `checkout` command. After you switch back you'll notice that your change no longer exists in the file. Don't worry! It's still there on your feature branch. If you're working with a remote repository that other people may have changed since you started working it's also a good ideal to `pull` the latest changes down:
```shell
 % git checkout master
 % git pull origin master
Already up-to-date.
```
At this point your master branch should be up to date with the latest changes in the remote repo (the changes out on github), so we should be safe to merge our changes in. 

### Merge your changes to `master`
We'll use the _merge_ comand to merge our feature branch into the `master` branch, and assuming all goes well you should see something like: 

```shell
 % git merge ignore_xyz
Updating 7792e50..8eafff2
Fast-forward
 Java.gitignore | 1 +
 1 file changed, 1 insertion(+)
```

## Pushing changes out
Since you'll want the world to see your changes, you will now push your local _master_ branch out to the _master_ branch on github. If you forked an existing repository up at the beginning this would be the _master_ branch there on your own personal fork of the project.

```shell
 % git push origin master
```
Since we pulled the latest just before we merged there hopefully shouldn't be any conflicts or errors. If there are errors git is generally pretty good about telling you what happened. One source of errors could be that someone else pushed a change into the master branch between the time you updated and the time you tried to push your change. Re-pulling _master_ and resolving any conflicts should take care of this. 

## Conflicts?!?!?
With multiple developers working in the same code there's always going to be a possiblity of a conflict. This just means that you and someone else have both edited a file at the same time and git isn't sure how to include both changes. Back when we switched to our `master` branch and pulled down the latest code we might have pulled down another developers changes to the same file we were working in. If this happens, when you try to merge you might see a message similar to:
```shell
 % git merge ignore_xyz
Auto-merging Java.gitignore
CONFLICT (content): Merge conflict in Java.gitignore
Automatic merge failed; fix conflicts and then commit the result.
```
Someone else modified Java.gitignore too. If we open up the file now, git has indicated the areas which need our attention:

```shell
<<<<<<< HEAD
*.abc
=======
*.xyz
>>>>>>> ignore_xyz
```
The area between the "HEAD" line and the "======" line indicates the changes that we pulled in from the remote repository while the changes below the "=======" line and the "ignore_xyz" line indicate our own changes. In this case, someone added "*.abc" at the same location we added "*.xyz". Since we don't want to mess up their work the solution would be to leave both lines in place. We then remove the "<<<<", "======", and ">>>>" lines to let git know we've sorted it out. 

```shell
 % git status
On branch develop
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)

	both modified:   Java.gitignore

no changes added to commit (use "git add" and/or "git commit -a")
```
Even though we've fixed the conflict we have to let git know by staging the combined file(s) and committing the results. 

```shell
 % git add Java.gitignore
 % git status
On branch develop
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

Changes to be committed:

	modified:   Java.gitignore
```
And of course we'll want to provide a useful commit message to indicate that the new commit was the result of a merge:

```shell
 % git commit -m "Merged Java.gitignore change for .xyz file extensions"
 % git push origin master
```