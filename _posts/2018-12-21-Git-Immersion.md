---
title: Git Immersion
date: '2018-12-21 17:15:00'
layout: post
tag:
- Git
category: blog
author: Anran Zhou
---

## Git Immersion
http://gitimmersion.com/index.html
### 1. Setup
* Setup Name and Email
	```git
		git config --global user.name "Your Name"
		git config --global user.email "your_email@whatever.com"
	```
	
* Setup Line Ending Preferences
```git
	// for mac
	git config --global core.autocrlf input
	git config --global core.safecrlf true
	// for windows
	git config --global core.autocrlf input
	git config --global core.safecrlf true
```

### 2. Basic Operations

|Features|Commands|
|:---:|:---:|:---:|
|Create a Project|git init|
|Checking Status|git status|
|Staging Changes|git add < Your filenames >|
|Committing Changes|git commit -m "< Your Comments >"|

Git works with changes not files.

### 3. History

|Features|Commands|
|:---:|:---:|:---:|
|Histories|git log|
|One line histories|git log --pretty=oneline|

We can see more options when using git log. `man git-log`. Here are some examples:
```git
	git log --pretty=oneline --max-count=2
	git log --pretty=oneline --since='5 minutes ago'
	git log --pretty=oneline --until='5 minutes ago'
	git log --pretty=oneline --author=<your name>
	git log --pretty=oneline --all
	git log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short
```

### 4. Aliases
* Git Aliases
	Git Aliases can be configured in the file `.gitconfig` under `$HOME`. Here are some examples:
	```git
		[alias]
		co = checkout
		ci = commit
		st = status
		br = branch
		hist = log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short
		type = cat-file -t
		dump = cat-file -p
	```
	
	
* Shell Aliases
	Shell Aliases can be configured in the file `.profile`.
	```shell
		alias gs='git status '
		alias ga='git add '
		alias gb='git branch '
		alias gc='git commit'
		alias gd='git diff'
		alias go='git checkout '
		alias gk='gitk --all&'
		alias gx='gitx --all'

		alias got='git '
		alias get='git '
	```

### 5. Getting Old Versions
The **checkout** command will copy any snapshot from the repository to the working directory.
```git 
	git checkout <hash-value>
	git checkout master
```
Tips:  We can make changes and commit them after checkout.
1. If we want to retain them, we can create a new branch using `git checkout -b <new-branch-name>`.
2. If we don't want to retain them, we can just perform another checkout.

### 6. Tagging Versions
Tag is a way to substitute hash values.

|Features|Commands|
|:---:|:---:|
|Create a Tag|git tag < tag-name >|
|Look up Tags|git tag|
|Delete a Tag|git tag -d < tag-name >|

Usage:
`git checkout <tag-name>`


### 7. Undoing  Changes

|Features|Commands|
|:---:|:---:|
|Undoing Local Changes|git checkout -- < file >|
|Undoing Staged Changes|git reset HEAD < file >|
|Undoing Committed Changes|git revert < HEAD/hash value> --no-edit|
|Delete Committed Changes|git reset --hard < HEAD/Tag/Hash Value >|
|Amend the Previous Commit|git commit --amend -m "< comments >"|

### 8. Files Operations

|Features|Commands|
|:---:|:---:|
|Add|git add < file >|
|Delete|git rm < file >|
|Move|git mv < file> < newFile >|
* git mv == git add  + git rm
	
### 9. Branches

|Features|Commands|
|:---:|:---:|
|Create| git checkout -b < branch >|
|Switch| git checkout < branch >|
|Merge| git merge/rebase < branch >|

* Resolve Conflicts when merging
* Merge vs. Rebase
	* rebase for short-lived, local branches.
	* merge for branches in the public repository.
	
 Becasue rebase will change the history of commit log.

* Using branches to develop by multi-developers.
 1. Create a new branch. 
 2. Write codes on that new branch. 
 3. If the master changes by others, merge master into the current branch. 
 4. merge back to the master.

### 10.  Multiple Repository
Repository may be on the local disk or on the remote server.

#### 1. Retrieve

|Features|Commands|
|:---:|:---:|
|Remote Repository Name| git remote|
|Remote Repository Details| git remote show origin|

#### 2. Create

|Features|Commands|
|:---:|:---:|
|Clone a Repository| git clone < object > < target >|
|Create a bare repository| git clone --bare < object > < target >.git|
|Adding a remote repository|git remote add < target > < object >|

#### 3. Branch Related 

|Features|Commands|
|:---:|:---:|
|retrieve branches including remote branches| git branch -a|
|Adding a Tracking Branch|git branch --track < branch > origin/< branch >|

### 11. Pull Changes 

|Features|Commands|
|:---:|:---:|
|Fetching Changes(not merge)| git fetch|
|Merge pulled changes| git merge origin/master|
|Fetching Changes(merge)| git pull |

* git pull == git fetch + git merge

### 12. Push Changes

|Features|Commands|
|:---:|:---:|
|Pushing Changes| git push < local branch > < remote branch >|