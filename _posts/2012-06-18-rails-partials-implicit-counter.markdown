---
author: sohaibbbhatti
comments: true
date: 2012-06-18 23:27:20+00:00
layout: post
slug: rails-partials-implicit-counter
title: Rails partials implicit counter
wordpress_id: 3
categories:
- Ruby on Rails
tags:
- Rails
- Ruby
- Ruby on Rails
---

While working on a Ruby on Rails project, I stumbled across an interesting thing.

    
    = render partial: 'product_line', collection: product_lines_with_brand(@result, brand)


In My view I was rendering the partial above. For styling reasons I required that after ever second time the partial is called, I should be adding a clearing div.

After spending some time to try to find a good solution, I stumbled upon something really neat that Rails provides by default; every partial rendered in such a fashion has a dynamic counter associated with it. In the case of the partial above, the name of the counter was **product_line_counter. **Basically the name of the partial with _counter being appended to the end of it.

So all I had to do was append the following snippet of code at the very end of the partial

    
     - if product_line_counter.odd?
       .clear
