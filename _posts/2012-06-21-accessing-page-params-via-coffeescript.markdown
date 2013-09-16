---
author: sohaibbbhatti
comments: true
date: 2012-06-21 19:32:12+00:00
layout: post
slug: accessing-page-params-via-coffeescript
title: Accessing page params via Coffeescript
wordpress_id: 46
categories:
- Javascript
tags:
- CofeeScript
- Javascript
- Jquery
---

For a recent project, I wrote a small snippet of code in coffee script which can be used to retrieve the value of a params in the current URL via passing an argument.

{% highlight coffeescript %}
paramValue = (name) ->
  name = name.replace(/[\[]/, "\\[").replace(/[\]]/, "\\]")
  regexS = "[\\?&]" + name + "=([^&#]*)"
  regex = new RegExp(regexS)
  results = regex.exec(window.location.href)
  unless results?
    ""
  else
    results[1]
{% endhighlight %}


I realized that when it comes to JavaScript, I have the most horrid practices and generally re-code the same functions over and over again for generic problems such as this.

I'll try maintaining a repo of convenience functions such as the one above in Github and add to it functions that I require to tackle generic problems. This practice should hopefully improve re-usability in my own code and might also prove useful to other developers.
