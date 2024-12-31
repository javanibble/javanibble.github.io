---
layout: post
title: "How to setup Git Merge and Diff Tools"
author: andre
categories: [ git ]
tags: [git, git config]
image: /assets/images/feature-images/feature-image-git.jpg
description: This post provides a step-by-step guide with a list of commands on how to setup the git mergetool and git difftool to make use of DiffMerge.
---

- Table of Contents
{:toc .large-only}

This post provides a step-by-step guide with a list of commands on how to setup the `git mergetool` and `git difftool` to make use of DiffMerge. 

## What is Git?
> “Git is a version control system for tracking changes in computer files and coordinating work on those files among multiple people. It is primarily used for source code management in software development, but it can be used to keep track of changes in any set of files. As a distributed revision control system it is aimed at speed, data integrity, and support for distributed, non-linear workflows.” ~ [Wikipedia][1]

## What is DiffMerge?
> “DiffMerge is an application to visually compare and merge files on Windows, OS X and Linux. Graphically shows the changes between two files. Includes intra-line highlighting and full support for editing. Graphically shows the changes between 3 files. Allows automatic merging (when safe to do so) and full control over editing the resulting file.” ~ [SourceGear][2]

## Install DiffMerge
The following is the single command required to install DiffMerge on macOS using Homebrew.
```shell
$ brew install --cask diffmerge
```

## Configure DiffMerge
The following commands will setup DiffMerge as the application to show changes and to solve merge conflicts
```shell
$ git config --global diff.tool diffmerge
$ git config --global difftool.diffmerge.cmd 'diffmerge "$LOCAL" "$REMOTE"'
$ git config --global merge.tool diffmerge
$ git config --global mergetool.diffmerge.cmd 'diffmerge --merge --result="$MERGED" "$LOCAL" "$(if test -f "$BASE"; then echo "$BASE"; else echo "$LOCAL"; fi)" "$REMOTE"'
$ git config --global mergetool.diffmerge.trustExitCode true
```

## Using DiffMerge
To use the DiffMerge application on the command line, use the following commands.
```shell
# diff the local file.m against the checked-in version
git difftool file.m

# diff the local file.m against the version in some-feature-branch
git difftool some-feature-branch file.m

# diff the file.m from the Build-54 tag to the Build-55 tag
git difftool Build-54..Build-55 file.m

# To resolve merge conflicts, just run git mergetool:
$ git mergetool
```

## Summary
Congratulations! You have successfully installed configured the git merge and diff tools to make use off DiffMerge. Follow me on any of the different social media platforms and feel free to leave comments.

[1]:https://en.wikipedia.org/wiki/Git
[2]:http://www.sourcegear.com/diffmerge/index.html