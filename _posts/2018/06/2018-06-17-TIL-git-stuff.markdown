---
layout: post
title:  "TIL: Some git stuff I'd been putting off"
date:   2018-06-17 20:15:00 -0000
categories: TIL
---
I've been using git for years now, but ironically enough I've never done anything with branching. For whatever reason the idea of creating branches has scared me, so I just never got around to learning how to use them. Turns out that they're super easy to use, and very useful.

### Basic stuff
- `git init` will create an empty git repo
- Git does not store multiple versions of the code
- Initial commit will create the master branch

### `git log`
- Shows the git commit history
- HEAD will follow the latest commit

### Checkout to specific commit
- `git checkout <commitId>`
- Can't add/commit after checked out. Commit does not match branch

### Switch back to master
`git master`
`git checkout master`

### Jumping back to Commit
- `git reset --hard <commitID>`

### Backout unsaved chnages
- `git checkout -- <filename>`

### Display all branches
- `git branch`

### Creating new branch
- `git checkout -b <branch_name>`
- Sets HEAD against new branch and master

### Merge back to master
- Change back to master branch first
- `git merge <branch_name>`

### Deleting a branch
- `git branch -D <branch_name>`

💚