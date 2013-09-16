---
author: sohaibbbhatti
comments: true
date: 2013-01-30 19:07:47+00:00
layout: post
slug: the-ruby-racer
title: The Ruby Racer
wordpress_id: 206
categories:
- Ruby
- Ruby on Rails
tags:
- libv8
- Ruby on Rails
- therubyracer
- Upgrade
---

These days at work I've been busy with upgrading the version of Rails of our app from 3.0.x to the latest 3.2.11. The upgrade process has been thoroughly enjoyable and intellectually rewarding albeit time consuming so for. However, while deploying the code onto the staging server I ran into an extremely frustrating problem.

Whenever I'd deploy my code onto the staging server I'd receive the error below. After trying virtually just about everything, I finally tried out one suggestion in the Github Issue list that I'd scoured upon(I'm afraid I do not have the the link).



	
  1. I first uninstalled the libv8 and therubyracer gem via the 'gem uninstall' command. 

	
  2. After this I installed 'therubyracer' gem manually via the 'gem install' command. This installs the libv8 gem automatically as it is a dependency.

	
  3. From the output generated I saw the version of therubyracer and libv8 installed and added those versions explicitly to my Gemfile.

	
  4. A bundle install later, this issue went away.


https://gist.github.com/4675624

I'm still unsure about the cause of this issue. Too tired to look into it right now, but perhaps some other time.
