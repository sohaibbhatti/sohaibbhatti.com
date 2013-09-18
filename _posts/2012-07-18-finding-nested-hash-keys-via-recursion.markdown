---
author: sohaibbbhatti
comments: true
date: 2012-07-18 18:59:33+00:00
layout: post
slug: finding-nested-hash-keys-via-recursion
title: Finding Nested Hash Keys via Recursion
wordpress_id: 121
categories:
- Ruby
tags:
- hash
- recursion
- Ruby
---

While integrating a SOAP service into some existing ruby code I required to verify whether certain information points were being obtained from the SOAP response. Unfortunately, the high degree of nesting in the Hash being formed was proving to be too troublesome to observe.(Ps for SOAP integration, Savon is an amazing gem!)

I decided to write a method to yield all the keys of the Hash as an array in a recursive manner. Here is the quick solution I came up with.

    
{% highlight ruby %}
Hash.class_eval %Q{
  def nested_keys
    global_keys = []
    keys.each do |key|
      if self[key].is_a? Hash
        global_keys +=  self[key].nested_keys << key
      else
        global_keys << key
      end
    end
    return global_keys
  end
}
{% endhighlight %}


Its something really simple and a slight variation of it can be used to pass in an input key which then returns the value of that key, assuming that all keys are unique ofcourse!

{% highlight ruby %}    
a = {:red=>{:foo=>:deepak, :blkeh=>{:mekh=>:fekh}, :boo=>:mekh}}
a.nested_keys # => [:foo, :mekh, :blkeh, :boo, :red]
{% endhighlight %}

