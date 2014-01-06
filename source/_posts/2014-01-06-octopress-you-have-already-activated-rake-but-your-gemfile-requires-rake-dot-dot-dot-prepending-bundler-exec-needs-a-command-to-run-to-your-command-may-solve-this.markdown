---
layout: post
title: "Octopress You have already activated rake but your Gemfile requires rake ... Prepending bundler: exec needs a command to run to your command may solve this."
date: 2014-01-06 05:47:47 -0500
comments: true
categories: 
---
Here I am setting up Octopress so that I could start blogging, and WHAM! I was immediately received with this error when I tried to run rake install

```You have already activated rake but your Gemfile requires rake 0.9.2.2. Prepending `bundle exec` to your command may solve this.```

This can be solved simply by changing the Gemfile.lock, changing the version Rake to the version that you have installed:

{% gist 8281230 %}

Or if you're running rake 0.9.6 you can just apply this patch.
