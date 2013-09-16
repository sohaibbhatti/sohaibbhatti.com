---
author: sohaibbbhatti
comments: true
date: 2012-11-11 16:42:46+00:00
layout: post
slug: issues-of-adding-control-flow-logic-in-respond_to-blocks
title: Issues of adding control-flow logic in respond_to blocks
wordpress_id: 149
categories:
- Ruby on Rails
tags:
- Bug
- controller
- Rails
---

The following code was written by my boss to simulate an issue arising with a production app that I've been working on at work.

https://gist.github.com/4055328

Can you identify any sinister issues lurking within this code?

Assuming that the responses is a json response and that @racer.name is indeed 'john',
the if condition should execute which would lead one to believe that @was_in_if_block would evaluate to true followed by the the rest of the code not to execute. However, if this code was spec'ed out(which indeed it is, to simulate the issue, [https://github.com/alisyed/RailsAnomalies](https://github.com/alisyed/RailsAnomalies)) we would have observed that @was_outside_if_block was being assigned true as well. In other words the return isn't working as expected.

The reason? Lets delve into Rails code!

The `respond_to` method invokes the important `retrieve_collector_from_mimes(mimes, &block)` which first evaluates the particular type of mime_types the controller action can respond to at both a controller level configuration for example:

    
    respond_to :json, :except => [ :edit ]


`` and also inspects the block passed to the respond_to method. The collector for the particular request is attempted to be found. Assuming that the the request is JSON for our case, the collector for our particular request will initially be assigned the format.json block in the if condition(It is important to note that the code inside the actual format blocks will not be executed yet) and since another format.json block exists, our collector will later on be assigned that block. This is carried out by the block.call(collector) statement.

https://gist.github.com/4055425

As the code in the format.json block isn't executed yet, @was_in_if_block will still have a value false, and the @was_outside_if_block will be assigned a value of true.

The format.json block will then execute, which is the last line of the respond_to method.
