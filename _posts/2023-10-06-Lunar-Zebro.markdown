---
layout: post
title: Lunar Zebro
date: 2017-04-06 13:32:20 +0300
description:  # Add post description (optional)
img: luna_zebro_swarm.jpg # Add image post (optional)
---


In this project, I am working in the AI team of Lunar Zebro, developping the path planning and obstacle avoidance methodology for a small lunar rover of the student team (in TU Delft).

### A bit about Lunar Zebro

Lunar zebro is a unique six-legged with the objective of operating in a swarm on the moon. The first mission will focus on walking 200 meters in one Lunar day autonomously with a single rover. 

Regrettably, owing to the confidential nature of the undertaking, not many details can be disclosed at this moment.

The path planning and obstacle detection module can be divided into smaller sub-modules. *write more here about the rover system breakdown*
![Rock detections](/assets/img/rock_detections.png)

Artificial Potential field is used due to its computational efficiency compared to many other path planning methods. 

Enhanced curl-free vector field has been added to the system in order to attempt to prevent local-minimum problems at some obstacles.


### Current possible additional research explorations.

Unfortunately, due to the computational power of the rover microcontrollers sampling based algorithms such as RRT cannot be used. 

Nonetheless, a scope for further research could be to observe if, with a combination of multiple rovers (and in turn the availability  of multiple micorcontrollers), the processor workload could be shared to find the possible paths. 

PLEASE CLICK THE IMAGE BELOW TO SEE A VIDEO ABOUT LUNAR ZEBRO

[![Lunar Rover Video](/assets/img/lunarzebro.jpg)](https://www.youtube.com/watch?v=JahFz2Oduk0)
