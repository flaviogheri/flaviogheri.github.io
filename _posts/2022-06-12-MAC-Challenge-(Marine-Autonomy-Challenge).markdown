---
layout: post
title: MAC Challenge (Marine Autonomy Challenge)
project_length: "3/5"
date: 2022-06-12 13:32:20 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: MAChallenge_boat.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Competition, Robotics, Maratime Engineering]
---
In this project, I, aside with my team, developed code for an autonomous vessel that would be capable of self navigation, obstacle avoidance and finding source of pollution using a "virtual pollution sensor", and, in theory, percieving ocean plastic.

Here is the link to the competition:

[![Marine Autonomy Challenge](https://your-image-url.com)](https://www.maritimeindustries.org/events/marine-autonomy-challenge-machallenge)

and an article from the university of southampton of my team :

[![Southampton Engineering Students Enter Marine Autonomy Challenge](https://your-image-url.com)](https://www.southampton.ac.uk/smmi/news/2022/11/15-southampton-engineering-students-enter-marine-autonomy-challenge.page)


The team was, called SMART, was formed by:
* Me - Flavio Gheri (at the time Mechanical engineer who was president of the Robotics society)
* Nefelie (Maratime Engineer with strong routes in machine learning and robotic)
* Chihiro (Master student who previously was part of the research wing of Japans ministry of defense)
* Prateek (Master student in Maratime engineering)
* Joe (Maratime engineering student who was developping a thesis on probabilistic localisation for autonomous vessels with Blair Thornton)

Prof [Blair Thornton](https://scholar.google.com/citations?user=fpLYlVwAAAAJ&hl=en&oi=ao) proposed me to join the team for my expertise in robotics. Other professors that were supervising are project included [Nicholas Townsend](https://scholar.google.com/citations?user=z9utG3sAAAAJ&hl=en&oi=ao) and [Stephen Turnock](https://scholar.google.com/citations?user=IRoMIokAAAAJ&hl=en&oi=ao).




## A little more on MAChallenge

MAChallenge is a bi-annual challenge open to student teams at UK universities. Each team is provided with a simulator to work on and then given the final boat on the day of the competition.
The competition is then carried out on a 2m catamaran.

<!-- ![I and My friends]({{site.baseurl}}/assets/img/MAChallenge_boat.jpg) -->

The competition is devised into 5 challenges, which are: 

### Challenge 1: Navigating a waypoint track

The USV is required to navigate smoothly around loop track using a series of GPS waypoints. The USV should pass within 1 metre of each GPS waypoint and mantain as small as possible average cross-track error.


### Challenge 2: Obstacle Avoidance

The USV is required to follow a loop track and reactively avoid stationary obstructons detected by a virtual sensor. The position of obstacles are provided during the run in the form of regularly updated TTM messages, with target range and bearing.


### Challenge 3: Berthing

The USV is required to approach berth from a given point and stop safely at the berth. This means that it must fully stop in the water at 1m from the berth and be parallel. 


### Challenge 4: Searching for Pollution

The USV is required to autonomously search and map an area of pollution. Concentration of the pollutant is given by a virtual sensor. The USV will then need to record and return the maximum values, and, consequently, the source.


### Challenge 5: Searching for surface 'targets'

The USV will be required to automatically search a specified area for a number of physical objects (such as milk bottles, buoys etc..).

## How Project was tackled


The vessel created a simple grid of waypoints in a given area in order to create an effective map (please look at PDM for my other exploration of more complex path planning techniques).  Due to water dynamics, secondary waypoints around the original waypoints are created for a smoother trajectory with less overshoot. With more time, trajectory planning using splines will be looked into instead.

![Mac_route_plan](/assets/img/MAC_planning.png)

As previously mentioned, this allowed the rover to create an effective pollution plot (fitting the points found to a gaussian distribution), and to find the source of the pollution. 

![pollution_map_1](/assets/img/MAChallenge.png)

![pollution_map_2](/assets/img/MAChallenge2.png)

Finally, since the gps coordinates are much to innacurate to do effective berthing, the laser range finder (single-beam lidar) was used. 

The beam points were used once the vessel was infront of the dock. Here, the line fitting is performed to trace a line to estimate the distance of the vessel.

Here is a shematic of how the vessel was designed to be able to berth.

![berthing](/assets/img/berthing_MAC.png)

Finally obstacle avoidance was envisioned to be done using potential fields, however this was not effectively completed in time (as the object recognition wasnt completly succesful). To see more about a project were this is more succesfully accomplished, please see the Lunar Zebro project.

Images about Obstacle avoidance techniques that we will implement: 

![potential_field](/assets/img/potential_field_MAC.png)





<!-- 
* Hexagon shoreditch beard
* Intelligentsia narwhal austin
* Literally meditation four
* Microdosing hoodie woke -->

