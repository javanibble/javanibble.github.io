---
layout: post
title: "Git Essentials"
author: andre
categories: [ git ]
tags: [git, git config]
image: /assets/images/feature-images/feature-image-git.jpg
description: "The Git Essentials article provides you with a brief introduction to Git. It provides an installation guide and command-line commands for different scenarios used within the management of source code during software development."
comments: true 
---

- Table of Contents
{:toc .large-only}

The Git Essentials article provides you with a brief introduction to Git. It provides an installation guide and command-line commands for different scenarios used within the management of source code during software development.

## What is Git?
> “Git is a version control system for tracking changes in computer files and coordinating work on those files among multiple people. It is primarily used for source code management in software development, but it can be used to keep track of changes in any set of files. As a distributed revision control system it is aimed at speed, data integrity, and support for distributed, non-linear workflows.” ~ [Wikipedia][1]


## Installation & Setup
The following links contain guides on how to install Git on your machine:
* [JavaNibble: How to install git on macOS using Homebrew](/how-to-install-git-on-macos-using-homebrew/)
* [JavaNibble: Git Commands - Initial Setup](/git-commands-initial-setup/)


## Git Common Scenarios
There are a number of common scenarios where developers make use of git to perform certain functions. It is through these
common scenarios that we get to appreciate the flexibility and power that git provides.

### Git Configuration
#### Configuration Locations
When reading, the values are read from the system, global and repository local configuration files by default, and 
options `--system`, `--global` and `--local` can be used to tell the command to read from only that location.

When writing, the new value is written to the repository local configuration file by default, and options `--system` or 
`--global` can be used to tell the command to write to that location. This means `--local` is the default.

<div style="text-align: center;">
<img width="400" src="https://www.javanibble.com/assets/images/posts/git-essentials/git_configuration.png">
</div>
<br/>
The following locations are applicable to macOS:
* System: The configuration is located at `/usr/local/etc/gitconfig`.  
* Global: The configuration is located at `$HOME/.gitconfig`.
* Local:  The configuration is located at `[local_repo]/.git/config`

---

#### Display Configuration
Display all the configuration properties and values together with the configuration file location. The `--show-origin` 
option augments the output with the origin type (file, standard input, blob, command line) and the actual 
origin (config file path, ref, or blob id if applicable)

```shell
# View all of the settings and the configuration file its defined in
$ git config --list --show-origin
```

---

#### Delete Configuration
If you want to delete all the `user.name` config values from the `global` configuration, use the following:
```shell
# Remove the line matching user.name from config file.
$ git config --global --unset user.name

# Remove all lines matching user.name from config file.
$ git config --global --unset-all user.name
```

If you want to delete the entire `user` object from the `global` configuration, use the following:
```shell
# Remove the given section from the configuration file.
$ git config --global --remove-section user
```

---

#### Git Initial Setup 
The initial setup of git is to customise the Git environment for your local machine. The initial setup is performed only
once on an environment. Your username and email address forms part of your identity that is used as part of the commit
messages, hence this should be configured.
```shell
# Set the username within the global configuration file
$ git config --global user.name "Star-Lord"

# Set the email address within the global configuration file
$ git config --global user.email "starlord@knowhere.com"

# Set the default text editor to be used when typing a message 
$ git config --global core.editor emacs

# Change the default branch from master to main.
$ git config --global init.defaultBranch main
```

---

### Change Git Commit
#### Change the last commit (Amend)
It happens more than often that a mistake was made to the last committed message, due to a typo or additional
information that was left out. This scenario focuses on correcting the mistake of the last commit message. This
overwrites your last command with a new one. Since this approach overrides the last commit in your local repository, it
will only work for the last commit and also if you have not yet published to the remote repository.
```shell
# Replace the tip of the current branch by creating a new commit. 
$ git commit --amend -m "Correct Message with additional info / fix."
```

Additional files or changes to existing files can also be added to the last commit.
```shell
# Add the additional file to the index
$ git add additional_file.txt

# Replace the tip of the current branch by creating a new commit. 
$ git commit --amend -m "Correct Message with additional info / fix."
```

The `--ammend` flag is rewriting the history and should not be used if you have pushed the commits to the remote
repository.

---

#### Undo one or more commits (Reset)
The `git reset` command can be used to reset your current HEAD branch to the specified revision. This allows you to undo
the last one or more commits.

![Git Reset](/assets/images/posts/git-essentials/git-command-git-reset.png){:.lead width="800" height="100" loading="lazy"}


The following command resets the current HEAD to the previous commit. The `--soft` flag does not touch the index file or
the working tree at all, but resets the head to <commit>. This leaves all the changes as uncommitted local modifications
in your working copy.
```shell
$ git reset --soft HEAD~1
```

The following command resets the current HEAD to the previous commit. The `--mixed` flag resets the index but not the
working tree and reports what has not been updated. This is the default action.
```shell
$ git reset --mixed HEAD~1
```

The following command resets the current HEAD to the previous commit. The `--hard` flag resets the index and working
tree. Any changes to tracked files in the working tree since <commit> are discarded.
```shell
$ git reset --hard HEAD~1
```

It is possible to not only undo the latest commit by using `HEAD~1` but to undo the commits to any other specified state
using the unique commit id `<commit>`.
```shell
$ git reset --hard <commit>
```

---

#### Undo effects of a commit (Revert)
The `git revert` command is used to undo the effects of a specific commit by recording the reversal of the effects in a
new commit. The `git revert` command will not discard any commits that came after the specified one, but only revert the
effects of the specified commit. None of the commits are deleted.

![Git Reset](/assets/images/posts/git-essentials/git-command-git-revert.png){:.lead width="800" height="100" loading="lazy"}


The following command revert the changes specified by a specific commit and create a new commit with the reverted changes.
```shell
$ git revert <commit>
```
---

### Remove Files

#### Remove Files from Index (Force)
The `-f` or `--force` option of the `git rm` command override the up-to-date check. These options can be used to force 
git to remove a file that has been modified since the last commit, or that was added to the staging area but not yet 
commited to the local repository.
```shell
$ git rm -f file1
```

#### Remove Files from Index (Cached)  
Remove files from the staging area (index), but leave the file within the working directory. Once removed from the 
staging area, it will be removed from the local repository, once the changes (removed files) are committed.

`git rm` removes files from both the working tree and the staging area, unless you tell it to just remove from the 
staging area with `--cached`.
```shell 
$ git rm --cached file1 file2
```

It is possible for files that should have been ignored by the `.gitignore` file, to have ended up in the staging area 
(index) and local repository. To remove all the files excluded by the `.gitignore` file, use the following command.
```shell
$ git rm --cached `git ls-files -i -c --exclude-from=.gitignore`
```

An alternative to the above command to remove files from the staging area (index), that should have been excluded by 
the `.gitignore` file, its possible to remove all the files and add them again. The `.gitignore` file will exclude the 
applicable files and directories.
```shell
$ git rm -r --cached .
$ git add .
$ git commit -m "Delete files matching .gitignore"
```

#### Remove Files from Index (Dry Run)
The `--dry-run` option of the `git rm` command don’t actually remove any file(s), instead it shows if they exist in the 
index and would otherwise be removed by the command.
```shell
$ git rm --dry-run file1
```
---

### Git Branches
#### View Branches
It is possible to view the branches within the local and remote repositories of Git. The branch that is currently used 
will have an asterisk `*`. 
```shell
# View branches in local git repository
$ git branch

# View both remote-tracking branches and local branches
$ git branch -a
```

#### Create a new Branch
There are a number of ways you can create a new branch in git. 

```shell
# Create a new branch based on the current HEAD
$ git branch <feature_branch>

# Create a new branch based on an existing one
$ git branch <feature_branch> <existing_branch>

# Create a new branch from a specific commit
$ git branch <feature_branch> a41dc75d

# Create a new branch from a specific tag
$ git branch <feature_branch> v3.1

# Create a new branch from a remote branch
$ git branch --track <feature_branch> origin/<remote_branch>
```

It is also possible to create a new local branch from a branch in a remote repository. The local branch with the name of
`feature_branch` will be created based on the remote branch `origin/<feature_branch>`. Git uses the same name for the 
local branch.
```shell
$ git checkout --track origin/<feature_branch>
```


#### Switch to a new Branch
Create a new branch named `feature_branch`. The first approach is to create a new branch using the `git branch` command,
and then to switch to the newly created branch using the `git checkout` command. The shortcut is to use the `-b`option
as part of the `git checkout` command to create and switch to the newly created branch all in one.

```shell
# Two-step method
$ git branch <feature_branch>
$ git checkout <feature_branch>

# Shortcut
$ git checkout -b <feature_branch>
```

After you have made changes to the files, you should commit the files and push the branch to the remote repository.
```shell
$ git push -u origin <feature_branch>
```
---

#### Merge a Branch
The following sequence of steps should be performed to successfully merge a `feature_branch` into the `master` branch.

It is important for your local repository is up to date before merging. The `git fetch` command retrieves information 
from the remote repository without impacting your files within your working directory. The `git branch -a` command is 
used to see if the master branch on the local repository is behind. If this is the case, the `git pull` command 
retrieves the changes.

```shell
# Retrieves information from the remote repository
$ git fetch

# List both remote-tracking and local branches
$ git branch -va

## Switch to the master branch
$ git checkout master

# Retrieve the updates from the remote repository
$ git pull
```

The `master` branch is now updated and the `git merge` command will join the history of the `feature_branch` branch with
that of the `master` branch. A new commit, also known as a `merge commit`, will be created in the `master` branch.

```shell
$ git merge <feature_branch>
```
---

#### Rename a branch
To rename a local branch to something new is very simplistic with Git.
```shell
# Rename a local checked out branch to a new name.
$ git branch -m <new-branch>

# Rename a local branch, that is not currently checked out, to a new name.
$ git branch -m <old-branch> <new-branch>
```

To rename a remote branch, you need a combination of the following commands.
```shell
# Delete the old branch in the remote repository
$ git push origin --delete <old-branch>

# Create a new branch in the remote repository
$ git push -u origin <new_branch>
````
---

#### Delete a branch
To delete a local branch, the `-d` flag is used. The branch must be fully merged in its upstream branch or in HEAD if no
upstream branch was set.
```shell
$ git branch -d <branch>
```

If the local branch contains commits that haven't been merged into any other local branches or pushed to a remote 
repository, its possible to force a delete of the local branch making use of the `-D` flag or the `-d -f` flags. The 
branch will deleted even if it contains unmerged / unpushed commits.
```shell
$ git branch -D <branch>
$ git branch -d -f <branch>
```

To delete a remote branch, the `git push` command is used with the `--delete` flag.
```shell
$ git push origin --delete <branch>
```
---

### Remote Repository
#### Download data from remote repository
It is important to retrieve the latest changes from the remote repository to your local repository. Both the `git fetch`
and `git pull` command download data from the remote repository, but with a difference.

The `git fetch` command retrieves information from the remote repository without impacting your files within your working
directory.
```shell
$ git fetch origin
```

The `git pull` command retrieves information from the remote repository and update the current HEAD branch with the
changes by updating the working copy files. It is possible for merge conflicts to occur.
```shell
$ git pull origin master
```
---

### Other
#### Change the author & email

Change the username and email address within the global settings of git located in the `~/.gitconfig` file.
```shell
$ git config --global user.name "Star-Lord"
$ git config --global user.email "starlord@knowhere.com"
```

Change the username and email address within the local repository settings of git located in the `[repo]/.git/config` file.
```shell
$ git config user.name "Star-Lord"
$ git config user.email "starlord@knowhere.com"
```

Change the author (user & email) as part of the commit command.
```shell
$ git commit --author="Star-Lord <starlord@knowhere.com>"
```

Change the author of the last commit that was performed on the current branch.
```shell
$ git commit --amend --author="Star-Lord <starlord@knowhere.com>"
```

Use the interactive rebase command to change the author in more than one commit.
```shell
$ git rebase -i -p <commit>

# The editor will open and mark all the commits you want to change the author to 'edit'.
$ git commit --amend --author="Star-Lord <starlord@knowehere.com>" --no-edit
$ git rebase --continue
```
---

## Git Commands Reference
Git is divided into high level ("porcelain") commands and low level ("plumbing") commands. This Git Essentials Article
only focus on the high level commands. 

**Setup & Config:**
* `git config` - Get and set repository or global options ([Reference](https://git-scm.com/docs/git-config))

**Getting and Creating Projects:**
* `git init` - Create an empty Git repository or reinitialize an existing one ([Reference](https://git-scm.com/docs/git-init))
* `git clone` - Clone a repository into a new directory ([Reference](https://git-scm.com/docs/git-clone))

**Basic Snapshotting:**
* `git add` - Add file contents to the index ([Reference](https://git-scm.com/docs/git-add))
* `git status` - Show the working tree status ([Reference](https://git-scm.com/docs/git-status))
* `git diff` - Show changes between commits, commit and working tree, etc ([Reference](https://git-scm.com/docs/git-diff))
* `git commit` - Record changes to the repository ([Reference](https://git-scm.com/docs/git-commit))
* `git notes` - Add or inspect object notes ([Reference](https://git-scm.com/docs/git-notes))
* `git restore` - Restore working tree files ([Reference](https://git-scm.com/docs/git-restore))
* `git reset` - Reset current HEAD to the specified state ([Reference](https://git-scm.com/docs/git-reset))
* `git rm` - Remove files from the working tree and from the index ([Reference](https://git-scm.com/docs/git-rm))
* `git mv` - Move or rename a file, a directory, or a symlink ([Reference](https://git-scm.com/docs/git-mv))

**Branching and Merging:**
* `git branch` - List, create, or delete branches ([Reference](https://git-scm.com/docs/git-branch))
* `git checkout` - Switch branches or restore working tree files ([Reference](https://git-scm.com/docs/git-checkout))
* `git switch` - Switch branches ([Reference](https://git-scm.com/docs/git-switch))
* `git merge` - Join two or more development histories together ([Reference](https://git-scm.com/docs/git-merge))
* `git mergetool` - Run merge conflict resolution tools to resolve merge conflicts ([Reference](https://git-scm.com/docs/git-mergetool))
* `git stash` - Stash the changes in a dirty working directory away ([Reference](https://git-scm.com/docs/git-stash))
* `git tag` -Create, list, delete or verify a tag object signed with GPG. ([Reference](https://git-scm.com/docs/git-tag))
* `git worktree` - Manage multiple working trees ([Reference](https://git-scm.com/docs/git-worktree))

**Sharing and Updating Projects:**
* `git fetch` - Download objects and refs from another repository ([Reference](https://git-scm.com/docs/git-fetch))
* `git pull` - Fetch from and integrate with another repository or a local branch ([Reference](https://git-scm.com/docs/git-pull))
* `git push` - Update remote refs along with associated objects ([Reference](https://git-scm.com/docs/git-push))
* `git remote` - Manage set of tracked repositories ([Reference](https://git-scm.com/docs/git-remote))
* `git submodule` - Initialize, update or inspect submodules ([Reference](https://git-scm.com/docs/git-submodule))

**Inspection and Comparison:**
* `git show` - Show various types of objects ([Reference](https://git-scm.com/docs/git-show))
* `git log` - Show commit logs ([Reference](https://git-scm.com/docs/git-log))
* `git diff` - Show changes between commits, commit and working tree, etc ([Reference](https://git-scm.com/docs/git-diff))
* `git difftool` - Show changes using common diff tools ([Reference](https://git-scm.com/docs/git-difftool))
* `git describe` - Give an object a human readable name based on an available ref ([Reference](https://git-scm.com/docs/git-describe))

**Patching:**
* `git diff` - Show changes between commits, commit and working tree, etc ([Reference](https://git-scm.com/docs/git-diff))
* `git rebase` - Reapply commits on top of another base tip ([Reference](https://git-scm.com/docs/git-rebase))
* `git revert` - Revert some existing commits ([Reference](https://git-scm.com/docs/git-revert))

**Debugging:**
* `git bisect` - Use binary search to find the commit that introduced a bug ([Reference](https://git-scm.com/docs/git-bisect))
* `git blame` - Show what revision and author last modified each line of a file ([Reference](https://git-scm.com/docs/git-blame))
* `git grep` - Print lines matching a pattern ([Reference](https://git-scm.com/docs/git-grep))


## Resources
* [Git Documentation](https://git-scm.com/doc)
* [Git Documentation - Downloads](https://git-scm.com/downloads)

[1]:https://en.wikipedia.org/wiki/Git
