---
layout: post
title:  "TIL: Adding VScode to PATH, the easy way"
date:   2018-05-14 19:45:00 -0000
categories:
  - Tools
tags:
  - vscode
---
Working on a side project tonight and ran into a problem that I've hit many times before: launching vscode from the command line. So many times I've wanted to just open a file or folder up in vscode from the command line, but have been too lazy to update my bash file to set it. Today I found out: there's no need to do that.

Vscode handles this for you now, right inside the editor. As outlined [in this stackoverflow post](https://stackoverflow.com/a/36882426/7595951), all you have to do is:

1. Open up vscode
2. Press `cmd` + `shift` + `P` to bring up the vscode console
3. Search for `install 'code'`
4. Hit enter and vscode does its magic

You're now good to go with opening either folders or files using `code` straight from the command line. No need to reload or restart terminal instances.

To open the current folder in a new instance of code, use `code .`.

To open a specific file with code, use `code <fileName>`.

Super easy, I wish I had done it a long time ago. So much time wasted...

💚