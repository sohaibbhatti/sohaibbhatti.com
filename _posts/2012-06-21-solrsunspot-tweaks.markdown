---
author: sohaibbbhatti
comments: true
date: 2012-06-21 07:01:15+00:00
layout: post
slug: solrsunspot-tweaks
title: Solr/Sunspot Tweaks
wordpress_id: 42
categories:
- Ruby on Rails
tags:
- Rails
- Ruby on Rails
- Solr
- Sunspot
---

I recently had to improve the searching functionality on an app that I was working on. The search engine being used was apache Solr via the Sunspot Gem.

The basic configuration only matches exact searches without any regard for pluralization, so for instance if the word "dogs" was being queried, "dog" wouldn't have been a match. Also partial matches i.e  After doing quite a lot of digging around I found the following filters which proved to be really helpful.

    
    <filter class="solr.NGramFilterFactory" minGramSize="4" maxGramSize="15"/>
    <filter class="solr.PorterStemFilterFactory"/>


The initial filter, breaks any given word to be indexed, into different tokens. In the example above the minimum size of each token would be 4 and the maximum, 15. So for instance,  if there exists a word "monkey", the word would be tokenized yielding "monk", "monke", monkey" and "monkeys". All mapping to the original word monkeys.

The second filter, implements the Porter stemming algorithm, removes all the suffixes from a particular word before indexing them via a fixed set of rules. The original paper of the algorithm can be read [here](http://tartarus.org/~martin/PorterStemmer/def.txt).

Next thing left, suggested words on mismatch. I'll be editing this post once I find a solution to this problem.
