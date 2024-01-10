---
layout: post
title: Machine Perception for Car assignment
date: 2024-01-12 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: how-to-start.jpg # Add image post (optional)
tags: [Machine Perception, Lidar, KF, BF] # add tag
---

In this project, as part of a coursework for ... lidar, radar and camera vision was combined to detect humans, and map them and the car in 3d space. 

This is done through ICP (on lidar points to find vehicle transformation/movement over time), machine learning (to recognize people), kalman filtering to reduce noise of human detections and car movement. Aswell as particle filtering.

![ROC curve of human detection](/assets/img/ROCurve.png)

![vehicle prediction](/assets/img/vehicle_prediction.png)

![vehicle prediction](/assets/img/vehicle_prediction.png)

![Camera Lidar Points](/assets/img/CameraLidarPoints.png)