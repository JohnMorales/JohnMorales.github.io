---
layout: post
title: "How to cherry pick git commit using Tig"
date: 2014-01-15 20:46:10 -0500
comments: true
categories: 
---


The problem
-----------
Recently I needed to grab a commit that was on a release branch and bring it over to the master branch. We weren't ready to merge the whole branch and but I needed a specific commit.  

I do not want to have a merge conflict when the release branch is merged back into master.

Solution
--------
Git supports this via cherry-pick. This approach allows git to know that the commit that was cherry picked can be skipped when merging the branch to the destination containing the cherry-picked commit.

I was able to use tig to accomplish this by doing the following:

checkout the destination branch:  `git checkout master`

then open `tig`

then press 'b' to see all the branches
{% img /images/all_branches.png %}

then select the branch that contains the commit you want

once you select the commit you want press 'P' (case sensitive)

{% img /images/cherry_pick.png %}

the commit should now be on master `git push origin` to push the change. 
