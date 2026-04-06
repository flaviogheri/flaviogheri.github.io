---
layout: single
title: "Imitation Learning with the SO-100 Robot Arm"
permalink: /projects/imitation_learning/
---

## Introduction

This project used the SO-100 robot arm to autonomously perform a simple **pick-and-place** task with imitation learning. I evaluated two policy families from the LeRobot ecosystem:

- **Action Chunking Transformer (ACT)**
- **Diffusion Policy (DP)**

The complete work covered the full pipeline: hardware assembly, teleoperation, data collection, policy training, and real-world evaluation.

## LeRobot

[LeRobot](https://github.com/huggingface/lerobot/blob/main/examples/10_use_so100.md) is an open-source robotics project by Hugging Face focused on making real-world robot learning more accessible through reusable tools, policies, and dataset formats.

The SO-100 setup in this project used both a **leader arm** (for teleoperation) and a **follower arm** (executing the learned policy).

<div style="text-align: center; margin: 1rem 0;">
	<img src="/images/so100_arm/example_image.jpeg" alt="SO-100 follower and leader arms" style="max-width: 70%; height: auto;" />
	<p><strong>SO-100 setup used for teleoperation and policy execution.</strong></p>
</div>

## Assembly Notes

The official LeRobot guide was the primary reference for assembly and setup:

- [SO-100 guide (LeRobot)](https://github.com/huggingface/lerobot/blob/main/examples/10_use_so100.md)

Helpful video references:

1. [Assembly Guide by Hugging Face](https://youtu.be/FioA2oeFZ5I?si=NQLH5s0lG2xQ5Dyu)
2. [Assembly Guide by Phospho AI](https://youtu.be/PG_EJAeNRfM?si=C1TQe3-gLkf0pnIV)

## Experimental Setup

The setup used a leader (blue) and follower (gray) arm, both clamped to the table. I kept enough separation between them so the cameras captured the follower workspace clearly and I could monitor execution from the laptop.

<div style="display: grid; grid-template-columns: repeat(2, minmax(220px, 1fr)); gap: 0.75rem; margin: 1rem 0;">
	<img src="/images/so100_arm/top.jpeg" alt="Top position setup" style="width: 100%; height: auto;" />
	<img src="/images/so100_arm/bottom.jpeg" alt="Bottom position setup" style="width: 100%; height: auto;" />
</div>

> **Important:** Clamping the arms is a safety requirement. In case of sudden or unstable motion, firm mounting prevents damage to people, hardware, and nearby equipment.

I used:

- an overhead camera for global workspace context,
- and a close-view camera for precise gripper/object interaction.

## Data Collection

Data collection was the most time-consuming stage. The procedure that worked best was:

1. Start each episode from a consistent rest pose and hold for 1-2 seconds.
2. Keep action timing consistent (approach, grasp, move, place, retreat).
3. Return to rest pose at the end of each episode.

> **Tip:** Keep the environment simple and consistent during initial collection before introducing variability.

### Experiment 1: Fixed Object, Multiple Start Locations

- 4 start locations around one target area
- 15 episodes per location
- **60 episodes total**

<div style="display: grid; grid-template-columns: repeat(4, minmax(120px, 1fr)); gap: 0.6rem; margin: 1rem 0;">
	<img src="/images/so100_arm/bottom.jpeg" alt="Bottom location" style="width: 100%; height: auto;" />
	<img src="/images/so100_arm/top.jpeg" alt="Top location" style="width: 100%; height: auto;" />
	<img src="/images/so100_arm/left.jpeg" alt="Left location" style="width: 100%; height: auto;" />
	<img src="/images/so100_arm/right.jpeg" alt="Right location" style="width: 100%; height: auto;" />
</div>

### Experiment 2: Different Object, Same Locations

- Same 4 start locations
- 10 episodes per location
- **40 episodes total**

### Performance Metric

I used success rate as the primary metric:

$$
	ext{Success Rate} = \frac{\text{Number of Successful Attempts}}{\text{Total Attempts}} \cdot 100\%
$$

<div style="text-align: center; margin: 1rem 0;">
	<img src="/images/so100_arm/perf_metric.png" alt="Successful versus unsuccessful attempts" style="max-width: 90%; height: auto;" />
	<p><strong>Unsuccessful attempt (left) vs successful attempt (right).</strong></p>
</div>

## Evaluation

### Training Specifications and Success Rates (Experiment 1)

| Model Type              | Model Name | Task         | No. of Episodes | Action Steps | Inference Steps | Success Rate (%) |
|-------------------------|------------|--------------|-----------------|--------------|-----------------|------------------|
| ACT                     | ACT_V1     | Pick & Place | 60              | 100          | -               | 100              |
| Diffusion (CNN)         | DFS_V1     | Pick & Place | 60              | 8            | 50              | 25               |
| Diffusion (Transformer) | DiT_V1     | Pick & Place | 60              | 8            | 100             | 50               |

### Policy Video Samples

<div style="display: grid; grid-template-columns: repeat(2, minmax(260px, 1fr)); gap: 0.8rem; margin: 1rem 0;">
	<video src="/images/so100_arm/video_example.mp4" controls muted loop playsinline style="width: 100%; height: auto;"></video>
	<video src="/images/so100_arm/video_example2.mp4" controls muted loop playsinline style="width: 100%; height: auto;"></video>
</div>

The videos above show representative policy rollouts from the evaluated setup.

## Theory: What is Imitation Learning?

Imitation learning is a way of teaching a robot from demonstrations rather than from manually written rules. Instead of explicitly designing every action, we collect examples from an expert and train a policy to imitate that behavior.

A simple formulation is:

$$
a_t = \pi_\theta(o_t)
$$

where \(o_t\) is the observation at time \(t\), \(a_t\) is the action, and \(\pi_\theta\) is the policy with learnable parameters \(\theta\).

In the simplest case, this becomes **behavior cloning**: the model is trained in supervised fashion to predict the expert action from the observed state or image. A common loss is:

$$
\mathcal{L}(\theta) = \sum_t \left\| \pi_\theta(o_t) - a_t^{*} \right\|^2
$$

where \(a_t^{*}\) is the demonstrated expert action.

### Improving Beyond Naive Behavior Cloning

Simple behavior cloning has a critical limitation: **compounding errors**. If the policy makes even a small mistake, it can drift into states not present in the training data, and subsequent predictions become unreliable. For robot tasks like object sorting, this quickly leads to failure.

To address this, recent work like **Action Chunking with Transformers (ACT)** predicts action sequences rather than single actions:

$$
\{a_t, a_{t+1}, ..., a_{t+H-1}\} = \pi_\theta(o_t)
$$

By predicting in chunks (e.g., 4-8 timesteps), the policy learns to plan ahead and recovers from small errors more gracefully. This significantly improves success rates on real hardware.

What makes imitation learning interesting in robotics is that it can bypass a lot of manual controller design. Instead of deriving the behavior analytically, the robot learns it from examples. At the same time, it is also challenging, because even small errors can accumulate over time and push the robot into states that were not present in the training data.

## Practical Notes From Training

What mattered most in practice:

- Consistent demonstrations were more important than model complexity.
- Camera placement had a direct impact on policy reliability.
- Recovery behaviors (small corrective motions) improved robustness.
- Mechanical repeatability (mounting, backlash, cable strain) affected data quality.

In short, this project reinforced that imitation learning performance is tightly coupled to system-level quality, not only neural network design.

## Future Work

Next improvements I plan to explore:

- broader task diversity and more object types,
- deeper analysis of diffusion-policy underperformance in this setup,
- bimanual extensions and mobile-base integration,
- larger datasets with controlled domain randomization,
- and stronger evaluation protocols across lighting and camera perturbations.

## Useful CLI Snippets

These commands were the most useful during setup and iteration.

### Create and activate environment

```bash
conda create -y -n lerobot1 python=3.10
conda activate lerobot1
```

### Find ports

```bash
python lerobot/scripts/find_motors_bus_port.py
```

### Teleoperation

```bash
python lerobot/scripts/control_robot.py \
	--robot.type=so100 \
	--robot.cameras='{}' \
	--control.type=teleoperate
```

Remove `--robot.cameras='{}'` when teleoperating with active cameras.

### Check camera index

```bash
python lerobot/common/robot_devices/cameras/opencv.py
```
