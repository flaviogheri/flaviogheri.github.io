---
layout: post
title: Machine Learning Project
project_length: "2/5"
date: 2023-10-20 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: daylight.gif # Add image post (optional)
tags: [machine learning, Neural Networks, DT, Image Processing] # add tag
---

For the final coursework of RO47002 (Machine Learning), I was to develop a machine learning model that could direct a robot towards a red box at different times of day.

Since the project was simplified to a given simulation, the task was to create a model resistant to the different hues that rapresented the different times of day in the simulation.
In order to do this, a simple model that could be run was designed for the robot, that was, at the same time, resistant to colour variations.

Although, in theory, this assignment could be done without a machine learning model, the purpose was to test our understanding of machine learning (and no supervised learning allowed) so it was done as such. 

For this project several steps were implemented: 

> 1. Feature Extraction
> 2. Fine-Tuning of Model
> 3. Model Evaluation
> 4. Presenting Solution

## Feature Extraction

In order to keep the model simple, 2 main group of features were to be evaluated: 
> 1. Red pixel values in the image (position of pixel with maximum red hue, mean position of red intensity and standard deviation of red hue across image)
> 2. Boundaries of shapes (using image processing techniques such as Canny edge extraction and probabilistic Hough)

### 1. Red Pixel Values

This was simply done by * talk about how red pixel values appeared to be quite distinct for the cube*


![histogram of image]({{site.baseurl}}/assets/img/image_processing.png)

* include more information about hyper parameter tuning of the neural network * 