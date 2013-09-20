---
author: sohaibbbhatti
comments: true
date: 2013-06-27 19:59:51+00:00
layout: post
slug: classes-vs-modules-for-morbidly-obese-models
title: Classes vs Modules for Morbidly Obese Models
wordpress_id: 214
categories:
- Ruby
- Ruby on Rails
tags:
- modules
- Rails
- refactoring
- Ruby
- service objects
---

The concept of Thin controllers and fat models is preached heavily to individuals who are just picking up Rails. However there is a thin line between being fat and morbidly obese. Quite often is it the case where models in a Rails app, especially the User Model, tend to be a 1000+ lines of bloated mess which results in a headache of scrolling up and down.

This issue can be addressed in multiple ways. Two of which(for a monolithic architecture) are using:

# Modules

The general practice is that developers create modules and start throwing methods present in the class that they're attempting to refactor into the modules that they've newly created. To be honest, in my opinion  this practice is analogous to throwing garbage from one room into other smaller rooms.

Some times developers get lazy and just throw the methods in a module or two. This doesn't serve any real purpose. Perhaps the models are clean, however the modules are now bloated.

Other developers on the other hand try to be a bit cheeky and create a crap ton of modules with very few methods in them. This results in the parent class in being something like this. So many includes just looks ugly!

{% highlight ruby %}
class User < ActiveRecord::Base
  include Billing
  include RegistrationMethods
  include Subscription
  include Socials
  ...
  ...
  # Imagine another dozen modules being included here
  ...
end
{% endhighlight %}

Furthermore the refactoring might make sense for the developer, however for the rest of the dev team, they'll have trouble figuring out from where each method is coming from. (My rule of thumb: Modules should almost always exist as gems, because atleast for me that is where I go out hunting for their code if I ever need to delve into it)

# Classes Ftw!

A better approach would be to break down the functionality into smaller classes that have  actual meaning. 

{% highlight ruby %}
class Subscription
  def initialize(user)
    @user = user
  end

  def subscribe!
    ...
  end

  def unsubscribe!
  end
end
{% endhighlight %}

By breaking down the functionality and collecting them into logical entities(OOP) you gain the following advantages.

* No More Grep Driven Development. Reading the code becomes very intuitive. I know exactly where to look in my code base to figure out the code.

* The interfaces are very clean and well-defined.

* Classes can be completely independent from Rails. TDD becomes uber fast as we do not need to require the evil spec_helper(i.e. Rails).(Thank you Gary of DAS for this. You've helped me a lot. My biggest gripe with you is that why did you have to go inactive!)

# Ending Notes

It is important to note that I'm in no way dissing modules, however like all good things in life they can be over abused.

However when it comes to refactoring fat models, I would almost always recommend extracting the logic into logical classes first.
