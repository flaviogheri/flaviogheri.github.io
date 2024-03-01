---
layout: post
title: Lunar Zebro
project_length: "4/5"
date: 2023-10-06 13:32:20 +0300
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

More extensive algorithms that use other particles in order to reduce potential problems from the local minima problem are further developed. The results are found to perform very well compared to other artificial potential fields, reaching above 95% of robusteness on the experiments made on lunar field simulations.

## SWARM Potential Fields

Currently, I am working on developping the swarm capabilities for the Lunar Zebro. To be more specific, 2 main challenges will be undertaken, one in this first year, that of developping path planning and obstacle avoidance of the swarm. 

The second part of the project, of which my thesis will be, in theory, developed around, will be to create a novel approach to improve localization and obstacle detection by leveraging cooperative stereo-vision of the lunar zebro in a swarm.

<!-- PLEASE CLICK THE IMAGE BELOW TO SEE A VIDEO ABOUT LUNAR ZEBRO -->


### Current Development of Swarm APF 

Potential fields are a very effective method of generating desired velocities for swarms as they are easy to control, allow for easy formations, can be formulated in a decentralized manner, all whilst being computationally efficient.

The current design of formation will be largely based upon [L.Barnes' paper](https://ieeexplore.ieee.org/abstract/document/4433724). Here the a series of potential fields are summed to create a robot formation around a target location. This is given by : 


The final potential field will result in something as the following:

![APF swarm field](/assets/img/lunar_zebro/potential_fields.png)

As the robots will be moving in a formation, influencing each other, and the central point will be following a trajectory. According to Barnes, the individual swarm agents should are much less susceptible to the local minima problem found in single agent APF.

*write about equations and code developed by team ...*


### Current research in Low-cost Swarm SLAM

*write about current research made ...*

### Lunar Zebro Structure

A simple block diagram of the rover structure for path planning is given below.

![Lunar Zebro Block diagram](/assets/img/lunar_zebro/block_diagram.png)


In order to make this workm a middleware (ROS Noetic), was used. This is done as to send and recieve information from the different components of the rover with ease. 

The current ROS architecture on the rover can be broken down as such: 

![ros graph](/assets/img/lunar_zebro/ros_graph.png)

<!-- [![Lunar Rover Video](/assets/img/lunarzebro.jpg)](https://www.youtube.com/watch?v=JahFz2Oduk0) -->
