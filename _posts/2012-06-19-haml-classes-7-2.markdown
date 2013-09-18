---
author: sohaibbbhatti
comments: true
date: 2012-06-19 05:41:34+00:00
layout: post
slug: haml-classes-7-2
title: HAML classes
wordpress_id: 30
categories:
- Ruby on Rails
tags:
- HAML
- Rails
- Ruby
- Ruby on Rails
---

Since the day I learned HAML, I developed this really bad habit. Whenever I've to add a div with a single class I would use the proper notation.

{% highlight haml %}
  .brandImageLogo
{% endhighlight %}

However, as soon as multiple classes arise, I'd use an awkward notation.

{% highlight haml %}
  div{class: 'brandImageLogo floatLeft center'}
{% endhighlight %}


However I trudged upon the 'proper way' of how to do this.

{% highlight haml %}
  .brandImageLogo.floatLeft.center
{% endhighlight %}


Just proves how important it is to keep reading up on things you believe you're comfortable with!
