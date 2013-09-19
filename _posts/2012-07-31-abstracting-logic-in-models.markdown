---
author: sohaibbbhatti
comments: true
date: 2012-07-31 03:44:17+00:00
layout: post
slug: abstracting-logic-in-models
title: Abstracting Logic in Models
wordpress_id: 124
categories:
- Ruby
- Ruby on Rails
tags:
- Rails
- Refactor
- Ruby
- Ruby on Rails
---

In the code base of the primary project I'm working on, (Moviepass; the Netflix equivalent for watching movies in theaters) some of the models were getting a bit too chunky. In our case, the User model had exceeded 1200 lines of code.

I decided it would be best to abstract chunks of related logic into separate modules.

So, for example in the class User.rb, modules are being included in the following manner.

    
{% highlight ruby %}
#=========================================================
#Methods related to tribune/cs preferences located here
include User::TribuneMethods
...
#======================================
{% endhighlight %}


The modules being referred to currently exist In the lib folder (realized that it would be best if this should remain in the app/models)

    
{% highlight ruby %}
module User
  module TribuneMethods
    extend ActiveSupport::Concern

    ...
  end
end
{% endhighlight %}


I decided that it would be best to leave all the validations and associations in the respective models, as I think its pretty useful to have a look at them in the model itself.

The reasoning for the nested modules was to make the namespace conventions a bit more informational, i.e. at a glance I can see that this belongs to the User Model. Its a matter of personal preference though.

On a side note, if such modules are being created by anyone, a quick look at ActiveSupport::Concern should be done. I might write about it in a later blog post.

Following such a scenario might not be the best idea in all scenarios, however, when the models become so bloated that they cease to be "fat" and move on to the morbidly obese, taking necessary action seems to be a good approach.
