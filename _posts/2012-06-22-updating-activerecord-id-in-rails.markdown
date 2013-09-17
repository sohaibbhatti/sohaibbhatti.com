---
author: sohaibbbhatti
comments: true
date: 2012-06-22 20:26:22+00:00
layout: post
slug: updating-activerecord-id-in-rails
title: Updating ActiveRecord Id in Rails
wordpress_id: 49
categories:
- Ruby
- Ruby on Rails
tags:
- Active Record
- Rails
- Ruby on Rails
---

Today a colleague and I were revising a schema of a Rails project. During which he wanted to make a certain assertion. In order to prove his point he required to change the id of a particular object of a model. The steps he carried out were

{% highlight ruby %}
pry(main)> m = Movie.first
=> #<QuantumMovie id: 14, title: "Forrest Gump", rating: "PG-13", photos: "00001401.jpg", advisory: "for drug content, some sensuality and war violence", stars: #<BigDecimal:fa8d70c,'0.0',4(8)>, created_at: "2011-09-06 05:16:29", updated_at: "2012-05-25 08:27:39", writer: "Winston Groom", director: "Robert Zemeckis", review: "", distributor: "Paramount Pictures", running_time: 140, hiphotos: "000014h1.jpg", video: nil, genre: "Drama", release_date: "1994-07-06", producer: "Wendy Finerman; Steve Tisch; Steve Starkey", official_site: "", cast: "Tom Hanks; Robin Wright; Sally Field; Gary Sinese; ...", delta: false, movie_type_id: 1, featured_through: nil, approved: true, average_rating: 4, playing: nil, multiple_reservation: false, view_count: 0, movieid: 14, type: "QuantumMovie">
pry(main)> m.update_attribute :id, 99999
=> true
pry(main)> m.reload
ActiveRecord::RecordNotFound: Couldn't find QuantumMovie with ID=99999 [WHERE `movies`.`type` = 'QuantumMovie']
from /home/sohaib/.rvm/gems/ree-1.8.7-2011.03@moviepass/gems/activerecord-3.0.7/lib/active_record/relation/finder_methods.rb:304:in `find_one'
{% endhighlight %}


This behavior is really interesting. Apparently modifying the id of an ActiveRecord object in Rails and trying to save it is not permitted.

I believe however, that instead of true, perhaps it would have made more sense to raise an exception of some sort as I can see people spending a hefty amount of time trying to debug such an issue if they ever come across it.

Lesson of the day: You can initialize an object with whichever id you want, however once persisted, modifying the id doesn't seem possible.
