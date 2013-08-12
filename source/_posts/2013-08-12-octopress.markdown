---
layout: post
title: "Octopress"
date: 2013-08-12 12:43
comments: true
categories: Others
---

Octopress Setup
===

Octopress is a framework designed by Brandon Mathis for Jekyll, the blog aware static site generator powering Github Pages. To start blogging with Jekyll, you have to write your own HTML templates, CSS, Javascripts and set up your configuration. But with Octopress All of that is already taken care of. 

###Setup Octopress
```
git clone git://github.com/imathis/octopress.git octopress
cd octopress    # If you use RVM, You'll be asked if you trust the .rvmrc file (say yes).
ruby --version  # Should report Ruby 1.9.3
```
#####Next, install dependencies.
```
gem install bundler
rbenv rehash    # If you use rbenv, rehash to be able to run the bundle command
bundle install
```
#####Install the default Octopress theme.
```
rake install
```
###Blog Posts

Blog posts must be stored in the source/_posts directory and named according to Jekyll’s naming conventions: YYYY-MM-DD-post-title.markdown. The name of the file will be used as the url slug, and the date helps with file distinction and determines the sorting order for post loops.

Octopress provides a rake task to create new blog posts with the right naming conventions, with sensible yaml metadata.

#####Syntax
```
rake new_post["title"]
```

new_post expects a naturally written title and strips out undesirable url characters when creating the filename. The default file extension for new posts is markdown but you can configure that in the Rakefile.

###Generate & Preview
```
rake generate   # Generates posts and pages into the public directory
rake watch      # Watches source/ and sass/ for changes and regenerates
rake preview    # Watches, and mounts a webserver at http://localhost:4000
```
###Deploying to Github Pages
```
rake generate
rake deploy
```
