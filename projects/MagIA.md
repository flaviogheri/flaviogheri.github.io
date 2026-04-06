---
layout: single
title: '"MagIA, let your imagination loose"'
permalink: /projects/MagIA/
---
<!-- 
<div style="text-align: center; margin: 2rem 0;">
  <video autoplay muted loop playsinline style="width: 100%; max-width: 1200px; height: auto; display: block; margin: 0 auto; border: 1px solid #ddd; background: #111;">
    <source src="/images/magia/animated_panorama.mp4" type="video/mp4">
    Your browser does not support the animated panorama.
  </video>
  <div style="font-size: 0.95rem; color: #555; margin-top: 0.75rem;">Animated panorama header demonstrating the generated open-world background experience.</div>
</div> -->

## Una Magia

In this project, I implemented ideas for my startup. Unfotunately due to University and work committments I never had time to fully complete the project. But with someone willing to complete the startup with me, hopefully I will be able to get it up and running. 

If you want to learn more about the Startup you can refer to *this website*. This blog post rather is aiming to give a general digest of both the tech stack that was thought up in order to develop the startup as well as the legal and distribution aspects that need to be thought out. Here is how the blogpost will be broken down to: 
1. Creating an Application - the tech stack - 
2. Including AI in the Application pipeline, - a how to - 
3. How to found a startup, legal aspects to take care of
4. How to distribute your product - cost reduction - cost reduction - cost reduction


### Chapter 1. The Tech stack

Coming from mechanical engineering to robotics, I skipped the entire usual introduction to html, css, javascript and general app development. To me, this is one biggg fuzzy area. Not just in the languages, but everything that is involved with it. 

As the focus of this project is mostly focued on learning about scaling a product into market. I wanted to keep the application simple (and scale the pipeline later). Therefore I wanted to avoid as much as possible everything around dev-ops. By keeping the requirements as light as possible (keeping most if not everything about the app in-app), the idea was twofold: 
    1. IP is both very expensive and bearocratic. This goes against the focus of the project. If I want to make sure no-one copies my product, I would have to include verification procedures, such as codes, specialized QR and IP or something. This is needlessly complicated. Therefore I will drop all that once the product grows enough where it is worth giving it a thought. 
    2. I am probably going to make mistakes in my pipeline. Therefore I want to avoid as much as possible the vunerabilities exposed to the user. 
    3. I want to avoid the complexities of having a large distributed network. Therefore no kubernetes, helm or any dev-ops. Again the focus is on creating a tech business not the tech stack. 
    4. I want to costs from servers as much as possible. The app isnt guaranteed to work. And if it does, I want it to be profitable as early as possible. Just to feel like an achievement. Having to pay to host the distribution of images in and out + other is simply not worth it.

For this reason, the app will be developed such that it can be ran offline. The following will therefore be required: 

A frontend
A backend

As the animations are likely much easier (and the scaling later), if I use something such as godot. The focus will be on developing a frontent that can communicate with godot. And then handle the animations via Godot. 

Main Plan: 

1. Frontend -> 
2. Backend -> Python (data processing) + godot (animation)

### Animated Open World Background

The first playable experience should feel like an open world generated from the user's drawings and GenAI production. The animated background is not just decoration — it becomes the game world itself, with the scene dynamically built from drawing inputs, style transfer, and procedural generation.

<div style="text-align: center; margin: 2rem 0;">
  <img src="/images/magia/demo_dancing_stickman.gif" alt="Demo dancing stickman" style="width: 90%; max-width: 900px; height: auto; display: block; margin: 0 auto; border: 1px solid #ddd; padding: 10px; background: #111;">
  <div style="font-size: 0.95rem; color: #555; margin-top: 0.5rem;">Demo of a drawing-animated character performing a simple dance.</div>
</div>

This gives a strong proof of concept: the user's page drawing can be turned into an animation directly in the app, with the same sketch becoming part of the world and story.

<div style="text-align: center; margin: 2rem 0;">
  <img src="/images/magia/boy_waving.gif" alt="Boy waving character asset" style="width: 90%; max-width: 900px; height: auto; display: block; margin: 0 auto; border: 1px solid #ddd; padding: 10px; background: #111;">
  <div style="font-size: 0.95rem; color: #555; margin-top: 0.5rem;">Example of a separated character asset that can be reused in a custom game world.</div>
</div>

From the same idea, animations and stories can be created in two ways: directly in the page drawing itself, as shown by the `demo_dancing_stickman.gif`, and later as separate reusable assets, as shown by `boy_waving.gif`. That means a story can start from a simple sketch on the page and then scale into a full set of characters and game assets that are later assembled into a custom world.

### Chapter 2. Initial Scaling

In order to invest the product, I had to make sure I wasn't just a mad man, but that people actually were interested in such as product as I am. To do this I had several focus groups in several countries: 
 - 1. Liectenstein 
 - 2. Austria
 - 3. Switzerland
 - 4. France (Toulouse)
 - 5. Italy (Pisa/Florence)

 
