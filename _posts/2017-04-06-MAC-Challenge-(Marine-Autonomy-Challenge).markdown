---
layout: post
title: MAC Challenge (Marine Autonomy Challenge)
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

Images about Obstacle avoidance techniques that we will implement: 

![Mac_route_plan](/assets/img/MAC_planning.png)

![potential_field](/assets/img/potential_field_MAC.png)


### Challenge 3: Berthing

The USV is required to approach berth from a given point and stop safely at the berth. This means that it must fully stop in the water at 1m from the berth and be parallel. 

Here is a shematic of how the vessel was designed to be able to berth.

![berthing](/assets/img/berthing_MAC.png)


### Challenge 4: Searching for Pollution

The USV is required to autonomously search and map an area of pollution. Concentration of the pollutant is given by a virtual sensor. The USV will then need to record and return the maximum values, and, consequently, the source.


These are some pollution maps that were estimated from the sensor values that were found when the vessel moved in the water.

![pollution_map_1](/assets/img/MAChallenge.png)

![pollution_map_2](/assets/img/MAChallenge2.png)

### Challenge 5: Searching for surface 'targets'

The USV will be required to automatically search a specified area for a number of physical objects (such as milk bottles, buoys etc..).

## How Project was tackled

To start 







<!-- 
* Hexagon shoreditch beard
* Intelligentsia narwhal austin
* Literally meditation four
* Microdosing hoodie woke -->

