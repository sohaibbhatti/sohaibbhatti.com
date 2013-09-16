---
author: sohaibbbhatti
comments: true
date: 2012-06-30 20:10:06+00:00
layout: post
slug: action-recognition-via-spatio-temporal-localized-templates-part-1
title: Action Recognition via Spatio-Temporal Localized Templates Part 1
wordpress_id: 80
categories:
- Computer Vision
tags:
- computer vision
- vision
---

Over the next few posts I'll be iterating over a project of mine, that I'd initially carried out in Matlab. I'll soon be trying to port over the project to Ruby, as I just found out that a wrapper for using opencv(a really famous computer vision library) is available for the ruby language. (Though when i'll be able to complete this project I'm not sure, as I'm still facing problems running opencv via the wrapper in ruby :) )

The original aim of the project was to be able to develop a system, that could observe the strikes of a cricket batsman and label what kind of a stroke or shot he is playing.

In this post we'll be looking at the basic steps of a generic computer vision based project.

**STEPS INVOLVED IN A GENERIC COMPUTER VISION SYSTEM:**

The diagram below is an extremely generic version of a flow diagram required for any Computer vision based project.

[![](http://sohaibbbhatti.files.wordpress.com/2012/06/steps_of_cv.jpg)](http://sohaibbbhatti.files.wordpress.com/2012/06/steps_of_cv.jpg)



	
  * **Image Acquisition: **




****As the name suggests, obtaining the data via a camera or file.






	
  * **Pre-processing: **




Before complex processing is performed on the data set, pre-processing is performed. Image processing techniques are used to perform tasks such as reducing the noise and enhancing the contrast on the data set. Also the scale-space representation can be modified so as to perform problem solving in a more optimal manner. Notable procedures include background subtraction, contrast enhancement, the application of filters such as dilation/erosion and smoothing for noise removal.






	
  * **Feature Extraction:**




Feature extraction involves detecting interest points in the now pre-processed data. Certain key points in frames and/or associated data derived from them have a higher correlation to the actual problem. Common procedures include Speeded up Robust Features(SURF), Spatio-Temporal Interest Points(STIP) and Scale-Invariant Feature Transformation(SIFT).






	
  * ** Detection/Segmentation:**




This stage involves the detection and pruning of the data by choosing those points which are deemed necessary for the task of the computer vision system. For instance, a system developed for face detection, will generally only select the significant interest points located on the face of the image. The remainder of the data will be siphoned out so as to reduce computational cost.




Statistical methods such as Principal Component Analysis (PCA) or other “intelligent” methods such as the use of neural networks can be used.






	
  * **Classifier**




Processing as required by the applications needs is performed in this stage on the reduced data set. In the case for our problem, this would be the use of a supervised learning system and training it with a data set to make it capable of recognizing actions in newly presented data (videos)
