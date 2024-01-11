---
layout: post
title: Machine_Perception_Assignement
date: 2024-01-12 00:00:00 +0300
description: In this project, as part of coursework for RO47004, Lidar, radar, and camera vision were combined to detect humans and map them, along with the car, in 3D space.
img: CameraLidarPoints.png
tags: [Machine Perception, Lidar, KF, BF] # add tag
---

In this project, as part of coursework for RO47004: lidar, radar, and camera vision were combined to detect humans and map them, along with the car, in 3D space.

This was achieved through ICP (on lidar points to find vehicle transformation/movement over time), machine learning (to recognize people), Kalman filtering to reduce the noise of human detections and car movement, as well as particle filtering.

![ROC curve of human detection](/assets/img/ROCurve.png)

![vehicle prediction](/assets/img/vehicle_prediction.png)

![vehicle prediction](/assets/img/vehicle_prediction.png)

![Camera Lidar Points](/assets/img/CameraLidarPoints.png)