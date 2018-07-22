---
layout: post
title:  "TIL: Merging git repos"
date:   2018-04-15 19:30:00 -0000
categories:
  - Coding
tags:
  - git
---
For whatever reason I don't like having a bunch of small repos under my github account. At the start of learning go I was creating a bunch of little folders for projects and committing them into github. Looking over my page, it was gettin pretty sloppy and hard to tell what was somehting worthwhile that I created and what was just lessons. So I decided I'd do a little house keeping

## Merging repos
In my case I had about 6 small repos sitting inside of my main `go/src/github/fuzzylimes` path that already had some work/commits done to them. Rather than just tossing that work and losing this history, I was looking for a way to merge those files in and get them coppied over.

A quick google search landed me at [this stackoverflow answer](https://stackoverflow.com/a/10548919/7595951).

Before using the flow on this page, there's a few extra things that need to be done first:

1. `mkdir -p my/new/repo`
2. `git init`
3. `touch tmp.txt`
4. `git add .`
5. `git commit -m "Initial commit"`
6. `git rm tmp.txt`
7. `git commit -m "Cleanup"`

Now that the repo has been started, you're good to move on to merging over the repos into the new repo. The flow is like this:

1. `cd /my/new/repo`
2. `mkdir project`
3. `git remote add project path/to/project`
4. `git fetch project`
5. `git merge --allow-unrelated-histories project/master`
6. `git mv * project`
7. `git commit -m "Moved to correct subfolder"`
8. `git remote remove project`
9. `rm path/to/project`

Rinse and repeat until all of the repos have been added over to the new one.

### Problem with subfolders
If you'll notice, I wasn't able to get the files over into their subfolder in one go. When I tried this method from within the subfolder, I would always get error messages telling me that the path didn't exist. Not sure why that was, and I couldn't find any answers for it on the page. So I bit the bullet and did the transfer manually.

If you can find a way to do it in one go, more power to you!
