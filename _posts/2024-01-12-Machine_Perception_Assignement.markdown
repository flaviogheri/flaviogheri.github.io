---
layout: post
title: Machine_Perception_Assignement
date: 2024-01-12 00:00:00 +0300
description: In this project, as part of coursework for RO47004, Lidar, radar, and camera vision were combined to detect humans and map them, along with the car, in 3D space.
img: CameraLidarPoints.png
tags: [Machine Perception, Lidar, KF, BF] # add tag
---

In this project, as part of coursework for RO47004: lidar, radar, and camera vision were combined to detect humans and locate humans and their tracks in 3D space.

More specfically Kalman filtering was used in order to estimate the positions of pedestrians on the ground plane. 

In order to do this several steps were implemented: 
1. A clas was created to convert the 2D camera bounding boxes (from mono-camera) to 3D (by using estiamtes of z-axis through transformations of lidar points in centre of body).

In another assignment, stereo camera was trafsormed with lidar and radar points to compare the accuracies of the different sensors: 

![Camera Lidar Points](/assets/img/CameraLidarPoints.png)


2. The motion of the vehicle (ego-motion compensation) was made in order to determine the homogenous transformation of the vehicle in the static world coordinate frame. More specifically, the transformation was made using ICP (Iterative Closest Point), with a groundplane removed using the segment_plane function (from o3d library).

3. ```Tracker``` and ```kf``` classes were created to apply a kalman filter to 2D birds-eye view pedestrian location measurements in a static world coordinate frame. 
More specifically the tracker was designed by assuming a linear movement for each human, and attributing the sensore measurements to tracks by checking if they fit within a gating threshold. If this is not the case, new tracks are created. If tracks are not updated (do not have any measurements within the threshold for given time period), the tracks are eliminated.


In previous projects, image processing and machine learning was made in order to create a algorithm that what look through an image and signal if a human was in the boxes or not. Below is a ROC curve showing the trained model:

![ROC curve of human detection](/assets/img/ROCurve.png)
<!-- 
Other filters 

![vehicle prediction](/assets/img/vehicle_prediction.png)

![vehicle prediction](/assets/img/vehicle_prediction.png) -->