---
name: Autonomous Driving Engines for F1/10
tools: [Python, Ros2, Rviz, NVDIA Jetson Orin]
image: ..\resources\projects\f1tenth\thumbnail.gif
description: We developed autonomous driving algorithms for F1/10 racing cars.
---

#  Autonomous Driving Engines for F1/10 Racing Car

## Table of content
[1. Reactive methods](#1-reactive-methods)<br>
[2. Perception, planing and control](#2-perception-planing-and-control)


## 1. Reactive methods
Reactive methods are control strategies that use real-time sensor data to generate immediate responses without relying on complex planning or mapping. These methods prove effective when an agent lacks prior knowledge about its environment. However, their drawback is that the actions they generate are often suboptimal. Furthermore, making them work typically involves intensive fine-tuning of various parameters, which may not perform well under different environmental variations.

### Wall-following
The very first algorithm we employed was PID wall-following. Its principle is straightforward: the robot navigates along the wall while maintaining a fixed distance. The PID controller adjusts the steering angle to keep the distance between the agent and the wall constant.  
<figure style="text-align: center;">
  <img src="..\resources\projects\f1tenth\wall-follow-levined-blocked.gif" alt="Single Image" width="400" />
  <figcaption>PID wall-following</figcaption>
</figure>
This algorithm has a relatively simple implementation; however, it demands extensive time for tuning the PID gains. Moreover, it is inefficient in handling environmental singularities—for example, it struggles with sharp turns and indentations. Finally, achieving high speeds is almost impossible, as evidenced by significant wobbling even at lower velocities, which would be exacerbated at higher speeds.


<!-- <figure style="text-align: center;">
  <img src="..\resources\projects\f1tenth\gap-follow-levine-blocked.gif" alt="Single Image" width="400" />
  <figcaption>Gap follow in no-obstacle map</figcaption>
</figure>
<figure style="text-align: center;">
  <img src="..\resources\projects\f1tenth\gap-follow-levine-obs.gif" alt="Single Image" width="400" />
  <figcaption>Gap follow in map with obstacles</figcaption>
</figure> -->
### Gap-following
By identifying the nearest obstacles or sharp disparities in the LIDAR data and masking out an area corresponding to the agent’s size, ggap-following algorithm defines gaps (open spaces) for navigation. The agent then moves toward the gap that is widest or extends the farthest.
<figure style="text-align: center;">
  <div style="display: flex; justify-content: center; margin-bottom: 10px;">
    <div style="margin-right: 10px;">
      <img src="..\resources\projects\f1tenth\gap-follow-levine-blocked.gif" alt="Image 1" width="400" />
      <p style="text-align: center;">Gap-following in obstacle-free map</p>
    </div>
    <div>
      <img src="..\resources\projects\f1tenth\gap-follow-levine-obs.gif" alt="Image 2" width="400" />
      <p style="text-align: center;">Gap-following in obstacle map</p>
    </div>
  </div>
  <!-- <figcaption>Main caption for both subimages</figcaption> -->
</figure>
Apparently, this algorithm allows the robot to move more smoothly and at higher speeds than wall-following. However, it still exhibits the inherent limitation of reactive methods, namely that the generated trajectories are suboptimal.






## 2. Perception, planing and control
<figure style="text-align: center;">
  <img src="..\resources\projects\f1tenth\pure-pursuit-slam-levine.gif" alt="Single Image" width="400" />
  <figcaption>Pure pursuit on levine map recorded by SLAM on real F1/10 car </figcaption>
</figure>