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

    
    .brandImageLogo


However, as soon as multiple classes arise, I'd use an awkward notation.

    
    div{class: 'brandImageLogo floatLeft center'}


However I trudged upon the 'proper way' of how to do this.

    
    .brandImageLogo.floatLeft.center


Just proves how important it is to keep reading up on things you believe you're comfortable with!
