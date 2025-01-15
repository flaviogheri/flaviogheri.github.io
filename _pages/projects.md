---
layout: archive
title: "Projects"
permalink: /projects/
author_profile: true
redirect_from:
  - /projects
---




Path Planning Assignment

In this project (part of coursework for RO47005), I, together with 3 other students, developed global and local planners from scratch, with the objective being for a quadcopter to safely maneuver around different environments in the PyBullet simulation. I specifically focused on developing the Velocity Obstacles algorithm (local planning).

The global planning algorithms that were developed were: RRT, RRT*, IB-RRT* (intelligent bi-directional), and A*.

As we tested the performance of the different global planners, we decided to keep to a single local planner, for which we chose the Velocity Obstacles algorithm (why pick a functioning method like MPC when you can go rogue and pick an obscure one?).

## What is Velocity Obstacles

Velocity Obstacles is a local obstacle avoidance method. It involves creating a velocity space of the ego-agent and other agents, checking whether the shapes constructed from their future potential positions may collide, and changing the trajectory of your vessel accordingly. The method assumes a constant velocity for the other vessel.

We can more formally write the velocity equation of two agents as:

$$
VO_{A|B} = \{ v \;|\; \exists t > 0 : (v - v_B)t \in D(x_B - x_A, r_A + r_B) \}
$$

Where \(A\) has position $(x_A)$ and radius $(r_A)$, and $(B)$ has position $(x_B)$, radius $(r_B)$, and velocity $(v_B)$.


