---
author: sohaibbbhatti
comments: true
date: 2012-06-19 18:42:16+00:00
layout: post
slug: variable-scopes-in-ruby
title: Variable Scopes in Ruby
wordpress_id: 38
categories:
- Ruby
tags:
- Ruby
---

Around a month back, a colleague of mine and I were playing around with nesting and variable scopes in ruby. Here is a small piece of code I wrote for understanding better about what is going on with variable scopes.

    
    A = 'I am A'
    module Foo
      B = 'I am B'
      puts Module.nesting.inspect
      class Bar
        C = 'I am C'
        puts Module.nesting.inspect
        module World
          D = 'I am D'
          puts Module.nesting.inspect
          puts ::A
          puts ::Foo::Bar::C
        end
      end
    end
    
    p A
    p Foo::B
    p Foo::Bar::C
    p Foo::Bar::World::D


While not in the scope a particular variable, the **:: **operator can be used to specify which scope this variable belongs to. So If we're currently outside module Foo, **Foo::Bar::World::D **can be used to access constant D.

The statments with a **::** right at the very start are used to set the current scope to root level. This can be observed in module world where **::A **is being used to access the constant defined outside of module Foo.

The code above generates the following output.

    
    [Foo]
    [Foo::Bar, Foo]
    [Foo::Bar::World, Foo::Bar, Foo]
    I am C
    "I am A"
    "I am B"
    "I am C"
    "I am D"


Oh and the nesting method is used to see the current level of nesting.
