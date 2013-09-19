---
author: sohaibbbhatti
comments: true
date: 2012-09-07 07:44:34+00:00
layout: post
slug: rails-memoization
title: Rails Memoization
wordpress_id: 132
categories:
- Ruby
- Ruby on Rails
tags:
- memoization
- Rails
- Ruby
---

Ever written a method that performs expensive computations? For example matching a particularly cryptic regular expression for any given input.

If the same method is being reused multiple times in the same code base, memoization might be able save your computer or server quite a few clock cycles. The concept is fairly simple but is often overlooked.

{% highlight ruby %}
 def answer_to_ultimate_question_of_life
   #perform some insanely computationally expensive task here
   #returns 42
 end

puts "#{answer_to_ultimate_question_of_life}"
puts "#{answer_to_ultimate_question_of_life} is not to be mistaken with the meaning of life!"
{% endhighlight %}


In the example above we can see that the method is being called two which, as you can guess, will perform all the necessary computations two times.

One way to solve this issue is using assigning the result of this method to a variable and then invoking the variable twice. If it is being used in different methods of a particular class, instead of using a variable an instance variable can be used. (@ans)

    
{% highlight ruby %}
ans ||= answer_to_ultimate_question_of_life
puts "#{ans}"
puts "#{ans} is not to be mistaken with the meaning of life!"
{% endhighlight %}


Rails however provides a really cool alternative to this issue; the Memoizable module. It can be found in the ActiveSupport gem and using it is really easy and in my opinion looks really clean.

{% highlight ruby %}
class SuperComputer
  extend ActiveSupport::Memoizable

  def answer_to_ultimate_question_of_life
    #perform some insanely computationally expensive task here
    #returns 42
  end
  memoize :answer_to_ultimate_question_of_life
end
{% endhighlight %}

Voila! You are now set to abuse this method as many times as you want to in a particular request. It even works on methods that expects arguments and caches the result based on the input arguments being passed.

**However! **caution needs to be taken If the cached method has some independant variables affecting its behavior. I.e. It would fail miserably if the output of the method is supposed to change with the current time, or if some random numbers are being used inside, as the result based on the inputs would always be that of what it was first computed to be.

Look at the crude example below. Its output will always change. Caching it will render the output of the method to always be incorrect except for the first time.

{% highlight ruby %}    
class HitchHiker
  def guide_to_galaxy(obj)
    DateTime.now
  end
end
{% endhighlight %}
