---
author: sohaibbbhatti
comments: true
date: 2012-09-10 10:25:17+00:00
layout: post
slug: meaningful-method-arguments
title: Meaningful Method Arguments
wordpress_id: 140
categories:
- Ruby
- Ruby on Rails
tags:
- arguments
- Ruby
- smells
---

In the code base of the project that I'm currently working on, there is a crucial method in the Reservations model namely allowed?

    
     def allowed?(return_errors = false, _user = user, time_frame=DateTime.now)


This method is screaming for a serious refactoring! The reason is pretty obvious

Since all the parameters it accepts are optional arguments, it can accept any combination of arguments. What if a user has to check whether a reservation is allowed for a specific time_frame? In order for us to pass the time_frame argument to the allowed method, we are being forced to pass the default values of the return_errors and _user local variables as well. This is a serious code smell.


## **Use Hashes!**


A really simple solution, that is used extensively is to pass the arguments in the form of a hash. e.g.

    
    def allowed?(args = {})
      args[:return_errors] ||= false
      args[:user] ||= user
      args[:time_frame] ||= DateTime.now
      ...
    end




## *args or args?


Let us suppose that return_errors is a mandatory argument in this method. We can go about tackling this problem via 2 different ways.

    
    def allowed?(return_errors, args = {})


- OR -

    
    def allowed?(return_errors, *args)
      options = args.extract_options! # returns the last hash being passed as an argument
    end


Both are more or less the same. The latter approach makes the code a bit more future secure. For example, if a new argument movie was to be introduced, we could implement the logic in the allowed method treating movies as args[0]. Then where ever in the code base this logic needs to be called, pass movie in the allowed method.

The primary advantage is that we would not need to make changes in other places where allowed? was previously being called and the movie argument isn't required

    
    allowed? return_errors, movie, options #movies required here. Pass as argument
    allowed? return_errors, options #Previously being used, can be left as it currently is.




## Argument names


Final point. How often have you stumbled upon scenarios where a method is declared in the following manner and when it is being invoked, is being done so by passing true to it?

Passing a meaningful argument is important for code readability, especially because there is a high likelihood that the file in which the method is being called isn't the same where it is being invoked. I generally solve this using symbols, as they will equate to true any ways.

    
    def allowed?(return_errors=false)
    allowed? true #What does this exactly do?
    allowed? :return_error_codes #This method returns the possible errors
