---
layout: single
title: "Drone Path Planning"
permalink: /projects/path_planning/
---

<a href="/projects/" class="case-back">← Back to Projects</a>

<div class="case-hero">
  <span class="case-eyebrow">Unknown Environment</span>
  <h1 class="case-title">Drone Path Planning</h1>
  <p class="case-summary">
    Global planner implementation using the Dijkstra algorithm for a quadrotor in a
    PyBullet simulation, ensuring safe maneuverability and collision avoidance.
  </p>
  <div class="tag-chips">
    <span class="tag">Python</span>
    <span class="tag">Dijkstra</span>
    <span class="tag">PyBullet</span>
  </div>
</div>

<div class="case-section" markdown="1">
<span class="section-num">01.</span>
<h2>The Concept</h2>

This project was developed for the *Planning and Decision Making* course (RO47005) in the
Robotics MSc at TU Delft. The objective was to engineer a robust global planner capable of
guiding a quadrotor safely through diverse, obstacle-ridden environments inside a
physics-based simulation.

The core challenge was implementing the **Dijkstra algorithm from scratch** and integrating
it cleanly into the PyBullet simulation environment to enable autonomous navigation in 3D
space.

</div>

<div class="case-section" markdown="1">
<span class="section-num">02.</span>
<h2>Technical Deep Dive</h2>

### Smart Grid Generation

The foundation of the planner is a voxel-based grid. The simulation space is discretized into
nodes, and each node is validated against the environment boundaries and obstacle positions.
What remains is a navigable graph the pathfinding algorithm can search over.

```python
def filter_grid(XYZ):
    indices_to_remove = []
    for i, point in enumerate(XYZ):
        # Check bounds
        if (X_BOUNDS[0] <= point[0] <= X_BOUNDS[1]) and \
           (Y_BOUNDS[0] <= point[1] <= Y_BOUNDS[1]) and \
           (Z_BOUNDS[0] <= point[2] <= Z_BOUNDS[1]):
            # Check collision
            if not euclideanDistance(point):
                indices_to_remove.append(i)
        else:
            indices_to_remove.append(i)

    return np.delete(XYZ, indices_to_remove, axis=0)
```

The grid resolution is a direct trade-off: a fine grid produces smoother, safer paths at a
higher search cost, while a coarse grid is fast but blunt around obstacles.

<div class="grid-compare">
  <figure class="grid-demo">
    <svg viewBox="0 0 200 200" role="img" aria-label="Fine resolution grid">
      <defs>
        <pattern id="fine" width="20" height="20" patternUnits="userSpaceOnUse">
          <path d="M 20 0 L 0 0 0 20" fill="none" stroke="#d4dae3" stroke-width="1"/>
        </pattern>
      </defs>
      <rect width="200" height="200" fill="url(#fine)"/>
      <rect x="80" y="60" width="60" height="60" rx="4" fill="#9aa6b6" opacity="0.85"/>
      <polyline points="20,180 20,120 60,120 60,40 160,40 180,20" fill="none"
                stroke="#2563eb" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"/>
      <circle cx="20" cy="180" r="6" fill="#16a34a"/>
      <circle cx="180" cy="20" r="6" fill="#dc2626"/>
    </svg>
    <figcaption>Fine grid — high resolution (0.1 spacing)</figcaption>
  </figure>

  <figure class="grid-demo">
    <svg viewBox="0 0 200 200" role="img" aria-label="Coarse resolution grid">
      <defs>
        <pattern id="coarse" width="40" height="40" patternUnits="userSpaceOnUse">
          <path d="M 40 0 L 0 0 0 40" fill="none" stroke="#d4dae3" stroke-width="1"/>
        </pattern>
      </defs>
      <rect width="200" height="200" fill="url(#coarse)"/>
      <rect x="80" y="60" width="60" height="60" rx="4" fill="#9aa6b6" opacity="0.85"/>
      <polyline points="20,180 20,120 60,120 60,40 160,40 180,20" fill="none"
                stroke="#2563eb" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"/>
      <circle cx="20" cy="180" r="6" fill="#16a34a"/>
      <circle cx="180" cy="20" r="6" fill="#dc2626"/>
    </svg>
    <figcaption>Coarse grid — low resolution (0.2 spacing)</figcaption>
  </figure>
</div>

Once the grid is built, Dijkstra expands outward from the start node, always visiting the
lowest-cost frontier node next, until it reaches the goal — guaranteeing the shortest
collision-free path through the discretized space.

</div>
