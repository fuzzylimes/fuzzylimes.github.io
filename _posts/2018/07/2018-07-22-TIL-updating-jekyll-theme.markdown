---
layout: post
title:  "TIL: Updating Jekyll Theme"
date:   2018-07-22 20:32:00 -0000
categories:
  - Coding
tags:
  - jekyll
---
If you haden't noticed, the blog got a big make over today! It was long overdue and I'm pretty excited with how it turned out. Today's blog post will be talking about that migration and the things that I learned from the migration.

### Until now...
When I first started out working with jekyll, I had wanted to try to figure out how it worked for myself, so I opted to go with the most basic theme possible and try to work through creating my own components and create my own modified theme.

I quickly realized that this wasn't what I wanted to be spending my time on, and started looking for different themes to use. However, when I went looking for themes supported by github, I found [this article](https://pages.github.com/themes/) that said that there were only ~10 supported themes for github pages. An I really didn't like any of them.

So for the last 9 months or so, I've just dealt with it... until yesterday when I started searching around again. As I'm starting to get more posts on my site, I figured I'd probably be worth looking into getting some sort of traffic to it. And so I went looking for themes again.

During that search, I found an [updated post](https://blog.github.com/2017-11-29-use-any-theme-with-github-pages/) which said that all themes would be supported by github pages now. Finally, time for a change.

After browsing around through some of the more highly rated jekyll themes, I came across the [So Simple Theme](https://github.com/mmistakes/so-simple-theme). This seemed to fit exactly what I wanted. Supported paging, displayed tags and categories. And, even supported post searching! Very cool.

### Setting up
So the `So Simple Theme` had a bit of a getting started section to it, but it really wasn't clear to me how I'd be able to just migrate using an existing theme... so I did what seemed the easiest to me and cloned the repo down.

> Note: This would have been super easy if I didn't already have a github pages repo setup. Then I'd only need to fork and change the name to the name of my github pages account.

With the theme downloaded locally, I started updating all of the template files based on the documentation. The theme does a good job walking you through all of the sections that require updates and what needs to be put into them.

I did run into one issue while I was setting this up, and that was with how the site needed to be structured. I originally started off by creating an entire subfolder called `blog` and putting all of the posts and components below it. I thought that this was how it needed to be done as that's how it was handled in the sample/example blog included in the repo.

What I quickly found out is that that doesn't work how I wanted it to. It basically sets an entirely different main route for your page by putting the /blog/ in front of everything. Maybe that's helpful for some people, but as this only serves my blog, I didn't want that to happen.

The other side effect from the `blog` folder was that a new `blog` category got added to every. Single. Post. Not what I wanted.

After a refresher on how `jekyll` projects are supposed to look, I updated the project to be flat, with everything located in the top of the directory. This made all of my pathing work as expected, though the the disorganization drives me crazy...

Last bit of house keeping that needed to be done was getting my old previous blog entries updated with the correct categories and tags that I wanted. So I copied over my `_posts` folder and made my way through each and every one of the posts (115 including this post now) and updated those values.

### Fighting paging... again...
As this theme has summary pages for the different categories and tags, which in turn display the FULL list of your posts, I wanted to see if I could get some sort of paging working for those. After reading, I saw that people were recommending to use the `jekyll-paging-v2` gem. So I spent about an hour getting that set up and switching over everything to use that new package.

...and I could never get it to work like I wanted to. Because of the some of the fancy logic that the template provides, I couldn't get the paging to work in any meaningful way. The only option seemed to be creating indvidual pages for every one of my categories and tags... and then implementing the paging there. And that sure wasn't going to happen.

Soilers: if that wasn't bad enough, when I finally uploaded the changes to gethub, I found that the `v2` gem isn't even supported when building. So I had to rip everything back out and migrate back to the old pagination gem and flip all of the old code back to use it. Ugh.

### Migrating
With all of the pages set up how I wanted them to be, I was ready to try to migrate over the files to the existing blog repo.

Before doing so, I made a branch of the current good working blog just so that I wouldn't lose it forever. You know, just in case.

I then did a brute force copy of all of the files from the cloned and modified repo over my existing github repo. This pretty much updated all of the existing files/folders and brought in everything new that I needed. Then it was just a matter of testing again and making sure it was still working. Whew, almost done.

Last steps were just the final push up to github. As I mentioned in the previous section, I quickly found out that pagination was broken and had to revert everything back to the old way. Once that was complete, everything was looking nice, shiny, and new.

### The take away?
Don't try to use unsupported gems in your gethub pages projects. They won't build correctly.

💚