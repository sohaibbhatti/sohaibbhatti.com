---
author: sohaibbbhatti
comments: true
date: 2013-02-03 11:21:06+00:00
layout: post
slug: bundler-issue
title: Bundler Issue
wordpress_id: 210
categories:
- Ruby
tags:
- bundler
- rvm
---

Today I came across a minor problem, an easy fix.

My aged computer has the tendency to reboot at the worst of times.While working on a personal project, it crashed yet again. After which I kept receiving the following error whenever I tried to run a bundle install

    
    fetcher.rb:164:in `load': marshal data too short (ArgumentError)


The fix was relatively simple. I deleted the gemset from RVM and installed all the gems again, most probably one of gems got corrupted due to the abrupt reboot.



	
  * rvm gemset delete <gem_name>

	
  * rvm gemset create <gem_name>


If anyone who does not use RVM encounters this problem, they should go ahead and empty the contents of the ~/.gem folder

This also served as a good excuse to upgrade my version of RVM to the latest which is a relatively simple process and can be viewed via the `rvm help` command.
