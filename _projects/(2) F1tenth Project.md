---
name: Auto-driving Engines for F1/10
# tools: [Python, Ros2, Rviz, NVDIA Jetson Orin]
image: ..\resources\projects\f1tenth\thumbnail.gif
description: We developed autonomous driving algorithms for F1/10 racing cars.
---

#  Autonomous Driving Engines for F1/10 Racing Car
*A big shoutout to my incredible teammates — Prakriti Prasad, Shreyas Muthusamy and Shubhodeep Aditya — who stood by me through an unforgettable semester. From countless sleepless nights of debugging to all the shared moments of frustration and small wins, I’ve learned so much from each of you.*

This is a compilation of the methods that we have developed for our F1/10 cars for the labs and races in the course ESE 6150 - Autonomous Racing Cars @ University of Pennsylvania.

<strong>* <em>Please note that all animations in this article are displayed at 2x speed.</em></strong>


## Table of contents
[1. Reactive methods](#1-reactive-methods)<br>
[2. Planning-based methods](#2-planning-based-methods)


## 1. Reactive methods
Reactive methods are control strategies that utilize real-time sensor data to generate immediate responses without relying on complex planning or mapping, making them effective when the agent lacks prior knowledge about surrounding environment. However, these approaches are quite sensitive to noise and uncertainty, have limited adaptability to complex scenarios, and often yield suboptimal behaviors.

### Wall-following
The very first algorithm we employed was PID wall-following. Its principle is straightforward: the robot navigates along the wall while maintaining a fixed distance. The PID controller adjusts the steering angle to keep the distance between the agent and the wall constant.  
<figure style="text-align: center;">
  <img src="..\resources\projects\f1tenth\wall-follow-levined-blocked.gif" alt="Single Image" width="400" />
  <figcaption>PID wall-following</figcaption>
</figure>
This algorithm has a relatively simple implementation; however, it demands extensive time for tuning the PID gains. Moreover, it is inefficient in handling environmental irregularities—for example, it struggles with sharp turns and indentations. Finally, achieving high velocities is almost impossible, as evidenced by significant wobbling even at a low speed, which would be exacerbated at higher speeds.


<!-- <figure style="text-align: center;">
  <img src="..\resources\projects\f1tenth\gap-follow-levine-blocked.gif" alt="Single Image" width="400" />
  <figcaption>Gap follow in no-obstacle map</figcaption>
</figure>
<figure style="text-align: center;">
  <img src="..\resources\projects\f1tenth\gap-follow-levine-obs.gif" alt="Single Image" width="400" />
  <figcaption>Gap follow in map with obstacles</figcaption>
</figure> -->
### Gap-following
By identifying the nearest obstacles or sharp disparities in the LIDAR data and masking out an area corresponding to the agent’s size, gap-following algorithm defines gaps (open spaces) for navigation. The agent then moves toward the gap that is widest or extends the farthest.
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
Apparently, this algorithm allows for much smoother motion and higher speeds than wall-following. Additionally, thanks to its smooth and stable motion, the robot can easily avoid obstacles while exploring an unknown environment (at a conservative speed). However, it still exhibits the inherent limitation of reactive methods, namely that the generated trajectories are suboptimal.



## 2. Planning-based methods
Reactive strategies are effective in well-structured and predictable environments but often struggle with local minima and unexpected oscillatory behavior. However, in racing, where even a few milliseconds can create huge difference, an optimal and efficient navigation is strictly required. Planning-based methods  bring us closer to this objective by leveraging available environmental information (e.g., maps, constraints) or prior experience (e.g., recorded paths), resulting in more stable and optimal performance.

### Pure pursuit
Given a pre-planned trajectory and the agent's ability to accurately locate itself in the environment  (e.g., via SLAM and particle filter), pure pursuit algorithm computes driving commands by targeting a point at a fixed look-ahead distance along the planned path.

<!-- <figure style="text-align: center;">
  <img src="..\resources\projects\f1tenth\pure-pursuit-slam-levine.gif" alt="Single Image" width="400" />
  <figcaption>Pure pursuit on Levine map attained by SLAM on real F1/10 car </figcaption>
</figure> -->

<figure style="text-align: center;">
  <div style="display: flex; justify-content: center; margin-bottom: 10px;">
    <div style="margin-right: 10px;">
      <img src="..\resources\projects\f1tenth\pure-pursuit-slam-levine.gif" alt="Image 1" width="400" />
      <p style="text-align: center; max-width: 400px; margin: 0 auto; word-wrap: break-word;">
        Pure pursuit on SLAM-estimated Levine map and trajectory from real F1/10 car
      </p>
    </div>
    <div>
      <img src="..\resources\projects\f1tenth\pure-pursuit-fastest.gif" alt="Image 2" width="400" />
      <p style="text-align: center; max-width: 400px; margin: 0 auto; word-wrap: break-word;">
        Enhanced pure pursuit with a smooth trajectory and dynamic speed control attained by filtering and interpolation
      </p>
    </div>
  </div>
  <!-- <figcaption>Main caption for both subimages</figcaption> -->
</figure>
Despite its suprising simplicity, this algorithm delivers superior speed and stability compared to reactive approaches. Additionally, developers can easily combine it with other methods to optimize the input trajectory or speed management, further improving lap times.
<br>
<br>
<div align="center"> <i>The project is currently in progress and will be updated in the near future.</i> </div>

<div align="center"> <i>If you have any questions or are interested in the project, please contact me for further information.</i> </div>