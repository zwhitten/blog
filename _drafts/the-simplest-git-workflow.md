---
layout: post
title: The Simplest Git Workflow
date: 2017-07-05 7:15:00 -0500
comments: false
---

### Why? 

I love git. It was a breath of fresh air coming from a heavier Version Control System at a previous job. Git makes coding dare I say, fun? 
Git is extremely powerful. For people unfamiliar with Git it can seem daunting or confusing, either because they're coming from another VCS or they've never used a VCS at all (Shouldn't they be teaching _something_ in schools these days?)

Below I'll outline what I think is one of the simplest workflows you can use on your teams or in your own personal development. The goal is to avoid using some of the more advanced git features which can (when used incorrectly) get developers into trouble. 

**Assumptions:**
- You have git installed and configured
- There is a remote repository of some kind you want to work with

### Optional Setup
If you don't already have a remote repository setup write access, you can easily fork an existing repository on github. 

1. Go to the github page for a project you'd like to contribute to, ex: [github/gitignore](https://github.com/github/gitignore)
2. In the top right corner click the `fork` button. This creates a copy of the repository under your account that you will have rull read/write access to. 
3. On your own repository page click the `Clone or Download` button to get the repository URL for use in the cloning step below.

### Getting Started

Great you're still here! We'll first want to pull down a git repository. As an example we'll use github's repo with a collection of gitignore files by language type. (If you created a fork in the optional setup replace the git URL below with the URL to your personal repository)

```shell
git clone https://github.com/zwhitten/gitignore.git
```

which should result in something like this:

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
cd gitignore
```

### Working on changes locally

### Pushing changes out

### Conflicts?!?!?
