---
layout: post
title: Lunar Zebro
project_length: "4/5"
date: 2024-03-06 13:32:20 +0300
description:  # Add post description (optional)
img: luna_zebro_swarm.jpg # Add image post (optional)
---


In this project, I am working in the AI team of Lunar Zebro, developping the path planning and obstacle avoidance methodology for a small lunar rover of the student team (in TU Delft).

### A bit about Lunar Zebro

Lunar zebro is a unique six-legged with the objective of operating in a swarm on the moon. The first mission will focus on walking 200 meters in one Lunar day autonomously with a single rover, with an aim of deploying more rovers in order to do swarm navigation and mapping of the lunar surface.

Regrettably, owing to the confidential nature of the undertaking, not many details can be disclosed at this moment.

The path planning and obstacle detection module can be divided into smaller sub-modules. *write more here about the rover system breakdown*
![Rock detections](/assets/img/rock_detections.png)

An in house development of APF has been implemented on the rover, increasing its ability to get to an end goal from ~60% in regular APF to ~95% on simulated lunar test bed environments created using telescope imagery. Not much can be yet disclosed about the method of navigation other than it exploits the ability to backtrack and take previous options, reducing the chances of getting stuck in local minima.



## SWARM Potential Fields

Currently, I am working on 2 main areas. The first being in updating and improving the software framework, in order for it to be perfectly operational and effective for IAC conference in Milan (International Austronautical Conference). This means updating the code so that is uses ROS 2 instead of ROS. Creating an improved sensor fusion and CNN in order to detect rocks (currently using labelled objects), and to localise their position using stereo vision. As well as creating additional features such that making new FSM (eg. navigating to batterystation when low on battery) and creating an external GUI in order to show participants what the rover is doing.

My second responsibility is that of developping the swarm capabilities for the Lunar Zebro. Here I am researching current advancements in swarm map building and planning and developping the technology with Lunar Zebro. With the final idea of having a swarm map of the lunar surface created using the swarm capabilities of the rovers in order to increase the reliability of the data (as stereo vision isn't so effective in itself).

<!-- PLEASE CLICK THE IMAGE BELOW TO SEE A VIDEO ABOUT LUNAR ZEBRO -->


### Current Development of Swarm APF 

Potential fields are a very effective method of generating desired velocities for swarms as they are easy to control, allow for easy formations, can be formulated in a decentralized manner, all whilst being computationally efficient.

The current design of formation will be largely based upon [L.Barnes' paper](https://ieeexplore.ieee.org/abstract/document/4433724). 

# Potential Fields for Swarm

Potential fields are a very effective method of generating desired velocities for swarms as they are easy to control, allow for easy formations, can be formulated in a decentralized manner, all whilst being computationally efficient.

A simple yet effective swarm control is given in [1]. Here a simple swarm formation control method is designed, where agents are successfully positioned with very little information about the rest of the swarm, that center of the swarm and their nearest obstacles (individual obstacle avoidance).

In order to do this, a general potential field made up of 3 fields (outside ring, inside ring, within ring), allow the general swarm formation to always maintain a position in an ellipse around a reference frame $(x_{c}, y_{c})$. Each of the potential field is modeled as a sigmoid function and has a series of weights that have to be tuned in order for the formation to work as intended.

In the paper, a static potential field is described. By modifying the weight $\gamma$ as a function of time we can allow the formation to move along a path. The potential field surface $f(x,y)$ is described as a bi-variate normal function: 

$$f(x,y) = e^{-(x-x_c)^2 + \gamma (y- y_c)^2}$$

The partial derivative of x,y is taken to calculate the heading of each velocity: 

$$ d_{x} = f(x,y)2(x - x_{c})$$
$$ d_{y} = f(x,y)2 \gamma(y - y_{c})$$

In order to attract the agents in an elliptical ring, 3 different differential fields are created, each composed by a sigmoid function which decays their effect when they are no longer relevant (see paper for more details), the fields can be segmented as :

- ($S_{in}$) - Field that pushes agents outside center ellipse
- ($S_{out}$) - Field that pushes agents towards inside of outer ellipse
- ($SGN*N$) - Field that pushes agents towards front of ring

The overall shape and potential can be seen in Figure 1. The equation that describes it is the following: 

\[
\begin{align*}
    \begin{bmatrix}
        v_x \\ v_y
    \end{bmatrix} &= (S_{in} - S_{out})\begin{bmatrix}
                                    dx \\ dy
                                \end{bmatrix} + SGN * N \begin{bmatrix}
                                                                    dx \\ dy
                                                                \end{bmatrix} \\
               &= (S_{in} - S_{out} + SGN * N)\begin{bmatrix}
                                                        dx \\ dy
                                                    \end{bmatrix}
\end{align*}
\]


![APF swarm field](/assets/img/lunar_zebro/potential_fields.png)

**Figure 1:** Final Potential Field

## Controlling Swarm Member Spacing

Additional Sigmoid functions can be used for the obstacle avoidance of each individual agent to its peers (member spacing), and of other obstacles. In the paper, for simplicity, it is assumed that the only obstacles are other members of the swarm. Allowing for the same limiting function to be effectively used. Further research on how effective using this method to get individual agents to avoid obstacles needs to be made.

$$ S_{avoid}(\alpha_{avoid}, r_{avoid}, \Delta R_{avoid})= 1 - \frac{1}{1+e^{\alpha_{avoid}(\sqrt{r_{avoid}-\Delta R_{avoid}})}}$$

Some parameters are to be optimized in order to fully successfully use the algorithm. In the paper, a method is not suggested. Nonetheless, by making $S_{in}(R^*)$ arbitrarily small, where $S_{in}(R^*) = \varepsilon$ then we can equate all limiting functions from the various radii of the ring and the $\varepsilon$ parameter.

$$\alpha_{in} = \frac{1}{\Delta R_{in}} \ln\left(\frac{1-\varepsilon}{\varepsilon}\right)$$

The same is repeated for the other limiting functions ($\alpha s$). By adding the Sigmoid for the obstacle avoidance for each individual agent, we find that the final equation, including the avoidance of other obstacles becomes: 

\[
\begin{align*}
    \begin{bmatrix}
        v_x \\ v_y
    \end{bmatrix} &= (S_{in} - S_{out})\begin{bmatrix}
                                    dx \\ dy
                                \end{bmatrix} 
                                + \sum^{size - 1}_1 S_{avoid} \begin{bmatrix}
                                    dx \\ dy
                                \end{bmatrix}+ SGN * N \begin{bmatrix}
                                                                    dx \\ dy
                                                                \end{bmatrix}
\end{align*}
\]

The paper used the following parameters. It is believed, however, that if this algorithm is to be chosen, that the parameters should be tuned for the Lunar Zebro.

*write about equations and code developed (maybe link github repo) ...*


### Current research in Low-cost Swarm SLAM

*write about current research made ...*

### Lunar Zebro Structure

A simple block diagram of the rover structure for path planning is given below.

![Lunar Zebro Block diagram](/assets/img/lunar_zebro/block_diagram.png)


In order to make this workm a middleware (ROS Noetic), was used. This is done as to send and recieve information from the different components of the rover with ease. 

The current ROS architecture on the rover can be broken down as such: 

![ros graph](/assets/img/lunar_zebro/ros_graph.png)

<!-- [![Lunar Rover Video](/assets/img/lunarzebro.jpg)](https://www.youtube.com/watch?v=JahFz2Oduk0) -->
