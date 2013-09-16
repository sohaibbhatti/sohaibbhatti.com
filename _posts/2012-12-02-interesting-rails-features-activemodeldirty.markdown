---
author: sohaibbbhatti
comments: true
date: 2012-12-02 22:20:39+00:00
layout: post
slug: interesting-rails-features-activemodeldirty
title: 'Interesting Rails Features: Accessing changed attributes values'
wordpress_id: 175
categories:
- Ruby
- Ruby on Rails
tags:
- Active Model
- Rails
- Ruby
---

This feature isn't used nearly as much as it deserves to be.

ActiveRecord objects keep a track of whether any of their attributes values have changed via the ActiveModel::Dirty module.

https://gist.github.com/4191292

Next time, when temporarily assigning variables the values of object attributes before modifying them, remember that this functionality is already provided by Rails in an elegant way.
