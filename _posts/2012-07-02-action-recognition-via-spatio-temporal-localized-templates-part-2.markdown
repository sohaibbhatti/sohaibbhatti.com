---
author: sohaibbbhatti
comments: true
date: 2012-07-02 13:31:51+00:00
layout: post
slug: action-recognition-via-spatio-temporal-localized-templates-part-2
title: Action Recognition via Spatio-Temporal Localized Templates Part 2
wordpress_id: 104
categories:
- Computer Vision
---

**The Data-set**

Oddly, the most daunting and frustrating part of the project was creating the data-set. Videos were cropped from the moment the ball left the hand of the bowler to the execution of the shot by the batsman. A total of 267 such videos from 3 different matches from the previous world-cup were made. I wish I could share the data-set however I believe that will not be legal :P. The dataset was subdivided into 6 different sub-categories namely Flick, Off-drive, Offensive, Pull, Slog Sweep and Sweep.

[![](http://sohaibbbhatti.files.wordpress.com/2012/07/shot_types.jpg)](http://sohaibbbhatti.files.wordpress.com/2012/07/shot_types.jpg)

Prior to the feature based approach, I was experimenting with a template based approach. i.e. adding colored markers on batsmen to aid the system. However that proved to be too trivial. The data-set though was made by us. Though extremely horrid in quality, whoever needs(highly unlikely as there are extremely excellent data-sets already present, KTH NADA being the first that pops in my mind) it can feel free to ping me.

[![](http://sohaibbbhatti.files.wordpress.com/2012/07/template_based.jpg)](http://sohaibbbhatti.files.wordpress.com/2012/07/template_based.jpg)

**PreProcessing**

**Histogram Equalization**

Histogram equalization is a common known technique used for “enhancing” the image contrast. Prior to histogram equalization, the vast majority of pixels in a particular image can be present in a narrow band of pixel value range. This renders the task of identifying individual “objects” to be arduous. After histogram equalization, the pixels are spread over the entire Gray-scale spectrum. I'm just giving a brief overview. However, if anyone feels that I should go a bit more in-depth leave me a message, I'd be glad to!

[caption id="attachment_107" align="aligncenter" width="540"][![](http://sohaibbbhatti.files.wordpress.com/2012/07/batting_color.jpg)](http://sohaibbbhatti.files.wordpress.com/2012/07/batting_color.jpg) Colored image from a video of a shot[/caption]

[caption id="" align="alignnone" width="540"][![](http://sohaibbbhatti.files.wordpress.com/2012/07/batting_gray.jpg)](http://sohaibbbhatti.files.wordpress.com/2012/07/batting_gray.jpg) Gray-Scale representation of the Image[/caption]

[caption id="attachment_109" align="aligncenter" width="540"][![](http://sohaibbbhatti.files.wordpress.com/2012/07/batting_histogram.jpg)](http://sohaibbbhatti.files.wordpress.com/2012/07/batting_histogram.jpg) Histogram Equalization of the same shot. Note: the players are a lot more distinct, then the rest of the background.[/caption]


