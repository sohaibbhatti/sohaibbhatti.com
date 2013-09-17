---
author: sohaibbbhatti
comments: true
date: 2012-06-26 06:51:08+00:00
layout: post
slug: importing-date-time-from-spreadsheets-in-ruby
title: Importing Date Time From spreadsheets in Ruby
wordpress_id: 54
categories:
- Ruby
tags:
- Rails
- Ruby on Rails
---

Yesterday I was facing an interesting problem. While importing data present in an xlsx file,  I noticed that dates present in the excel file were being imported as numerical floats. My original code below

    
{% highlight ruby %}
DATE_COL = 10
2.upto(10) do |i|
  ...
  excel_file = Excelx.new("#{Rails.root}/temp/final_cand/khi_counsel_list.xlsx")
  date_ar = excel_file.cell(i, DATE_COL).to_formatted_s(:long)
end
{% endhighlight %}


After a quick google, I found out the float being returned was the number of days that have elapsed since (Dec 30, 1899). I went ahead and modified my code to the following after which everything started working fine.

    
{% highlight ruby %}
date_ar = (DateTime.new(1899,12,30) + excel_file.cell(i, DATE_COL).days).to_date.to_formatted_s(:long)
{% endhighlight %}
