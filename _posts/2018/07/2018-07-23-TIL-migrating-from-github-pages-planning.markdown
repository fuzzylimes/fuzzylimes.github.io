---
layout: post
title:  "TIL: Migrating From Github Pages: Planning"
date:   2018-07-23 22:15:00 -0000
categories:
  - Coding
tags:
  - jekyll
---
After a lot of thought, I decided I wanted to try to bring the blog off of github pages and over to my own hosted solution. I've pretty much run ut of time this evening to talk through the whole process, but I did want to at least outline what the process looked like for me. I'll be expanding on this in days to come after I get everything sorted out. Until then, the blog will still be up here, as well as on the new site.

### The Process
Here were the basic steps that I had to follow this evening:
1. Clone github repo over to new bitbucket repo
2. Set up new subdomain for site
3. Request new ssl certificates for the new subdomain
4. Clone over the new repo to my hosting server
5. Install ruby on the server
6. Install dependent gems
7. Set up nginx to serve the static site
8. Fight with the template for 2 hours to getting all parts of it working

And unfortunately there's still so much more to be done. I really want to set up a pipeline to have the server autobuild on every push, so I'll be working through that tomorrow.

#### In the meantime, [blog.fuzzylimes.net](blog.fuzzylimes.net) is now live!

💚