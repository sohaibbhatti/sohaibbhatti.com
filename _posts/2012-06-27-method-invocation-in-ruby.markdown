---
author: sohaibbbhatti
comments: true
date: 2012-06-27 19:11:39+00:00
layout: post
slug: method-invocation-in-ruby
title: Method Invocation in Ruby
wordpress_id: 57
categories:
- Ruby
tags:
- Ruby
---

Lets have a look at the code below. Any idea to what the output will be?

{% highlight ruby %}
    
module Foo
  def print_salutations 
    hello
  end 
  def hello
    p 'hello from Foo'
  end
end

module Bar
  def hello
    p 'hello from Bar'
  end
end

class MyClass
  include Foo
  include Bar
end

MyClass.new.print_salutations
{% endhighlight %}


Whenever a module is included into a class, Ruby converts that module into an anonymous Class and adds it as a parent to the class it is being included in. If we traverse through all the parents of a Class, we'll be ending up at the BasicObject class. (Ruby 1.9+)

    
{% highlight ruby %}
ruby-1.9.2-p290 :021 > MyClass.ancestors => [MyClass, Bar, Foo, Object, Kernel, BasicObject]
{% endhighlight %}


The illustration below depicts the ancestor chain for MyClass described above. Now comes the fun part:

[![](http://sohaibbbhatti.files.wordpress.com/2012/06/method_invocation_wide.jpeg)](http://sohaibbbhatti.files.wordpress.com/2012/06/method_invocation_wide.jpeg)

Whenever a method is invoked on My Class, a search of that method will be performed in MyClass. If no match is found, a search for an implementation of the method will be performed on its direct ancestor and so on, till Basic Object.

So for the example above, since MyClass doesn't have print_salutations defined in it, Bar will be searched for print_salutations. This will again yield nothing and a further lookup will be performed in Foo. Here a match is found. Here a call to the method hello is performed.

Again a search of hello will be performed from MyClass to all its ancestors; the first match  being found in Bar and voila 'hello from Bar' is printed.

If in the case a method that isn't defined anywhere in the ancestor chain of MyClass is invoked, after failing to find a match till BasicObject, Ruby will then begin searching an implementation of the method_missing method in the ancestor chain in the same manner.
