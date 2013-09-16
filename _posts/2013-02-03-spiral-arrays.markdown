---
author: sohaibbbhatti
comments: true
date: 2013-02-03 17:35:03+00:00
layout: post
slug: spiral-arrays
title: Spiral Arrays
wordpress_id: 187
categories:
- Ruby
tags:
- random code
- spiral array
---

Out of sheer boredom I decided to look through some of my old code and came across my spiral array implementation.

The spiral array problem is generally used as an interview question to check how strong the recursion skills of the candidate is. Given a matrix(2 dimensional array) we need to write code that prints out the matrix in a clockwise spiral fashion.

    
     
       1 2 3
       4 5 6  => 1 2 3 6 9 8 7 4 5
       7 8 9


This can recursively be solved by invoking methods that draws L shapes. Initially a method can be invoked that returns an L shape ranging from the top left to the bottom right of the matrix. Our problem space is reduced as a consequence.

Strikes represent elements that have been printed by a method call.

    
      <span style="text-decoration:line-through;">1</span>  <span style="text-decoration:line-through;">2</span>  <span style="text-decoration:line-through;">3</span>  <span style="text-decoration:line-through;">4</span>  <span style="text-decoration:line-through;">5</span>
      6  7  8  9 <span style="text-decoration:line-through;">10</span>
     11 12 13 14 <span style="text-decoration:line-through;">15</span>   => 1 2 3 4 5 10 15 20 25
     16 17 18 19 <span style="text-decoration:line-through;">20</span>
     21 22 23 24 <span style="text-decoration:line-through;">25</span>


The top left to bottom right L shape method will invoke a method to print an L shape from the bottom right to top left of the reduced matrix. These methods keep calling one another until the size of the problem matrix is 0 at which point we can terminate the recursion.

    
    <span style="text-decoration:line-through;"> 6</span>  7  8  9
    <span style="text-decoration:line-through;">11</span> 12 13 14   => 24 23 22 21 16 11 6
    <span style="text-decoration:line-through;">16</span> 17 18 19
    <span style="text-decoration:line-through;">21</span> <span style="text-decoration:line-through;">22</span> <span style="text-decoration:line-through;">23</span> <span style="text-decoration:line-through;">24</span>


The ruby code for this problem can be found on my [github](https://github.com/sohaibbhatti/spiral_array)
