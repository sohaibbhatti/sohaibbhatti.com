---
author: sohaibbbhatti
comments: true
date: 2012-12-01 23:37:29+00:00
layout: post
slug: appending-pivotal-tracker-story-ids-to-git-commits
title: Appending Pivotal Tracker story Ids to git commits
wordpress_id: 166
categories:
- Git
- Ruby
tags:
- git
- hook
- pivotal story
- pivotal tracker
- productivity
- Ruby
- script
- software
- technology
---

At work, we've adopted the habit of using Pivotal Tracker's hooks to keep a track of Git commit messages in the form of comments corresponding to their relevant pivotal stories. The advantage of this is that all other developers are aware of what is going on and the clients can also get a rough estimate of which features are currently in progress. Comments of the git commits are added by appending the pivotal story id in the git commit messages. e.g.

    
    [#pivotal_id]: git message


This workflow proved to be rather annoying as I'd be forced to look at the pivotal story id from Pivotal Trackers website before I'd prepend it to the git commit message. I decided to automate this procedure so that I shouldn't be worrying about such trivial tasks.

Here is the solution that I came up with. It makes use of git hooks to prepend the pivotal story id to the git message right after I make my commit.(the commit-msg hook)

https://gist.github.com/4185833

This script relies on the fact that when the `git branch` command is used, the current branch name has an asterisk right before the branch name. The regular expression being used to assign branch_name a value is responsible for detecting the asterisk branch.

Once the branch name is found, a simplistic format is used to embed the pivotal id into the branch name(Shown in the beginning comments). Since we're using a fixed format a regular expression for extracting the pivotal story id can easily be extracted. If the pivotal story id is found, the script then joins it with the git commit message.

This script is proving to be a great time saver. Currently it doesnt support multiple pivotal story id's. e.g.

    
    [#pivotal_id_1, #pivotal_id_2]: commit_msg


I'll add this functionality whenever I find the need for it. But for now I'm happy with the functionality as it is.

This script can be found on github along with usage instructions over [here](https://github.com/sohaibbhatti/productivity-scripts).
