---
author: sohaibbbhatti
comments: true
date: 2012-07-17 08:41:35+00:00
layout: post
slug: ruby-deep-copy
title: Ruby Deep Copy
wordpress_id: 115
categories:
- Ruby
tags:
- clone
- deep copy
- dup
- Marshal
- Ruby
- shallow copy
---

The fundamental difference between the dup and clone method provided by ruby is that dup  doesn't copy the eigenclass. Also it does not copy the frozen state of the object in question.

Both are shallow copies.

    
    class Testing
      def hello
        p 'calling from class'
      end
    end
    
    foo = Testing.new
    def foo.hello
      p 'calling from singleton'
    end
    
    s.clone.hello # => 'calling from singleton'
    s.dup.hello  # => 'calling from class'
    
    foo = {:testing => {:cool => 'swell'}}
    foo_clone = foo.clone
    foo_clone[:testing][:cool] = 'not cool'
    #foo[:testing][:cool] Will now be 'not cool' as well


This leads us to the question of how to perform a deep copy. The Marshal Module is used for this!

    
    foo_dump = Marshal.dump(foo)
    foo_clone = Marshal.load(foo_dump)
