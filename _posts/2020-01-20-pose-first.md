---
layout: post
title:  "Data Collection & Pose Estimation"
date:   2020-01-20 1:10:35
author:  Caravel Team
---

Today we hope to post our first official update to the project. We recently ordered a simple, cheap Logitech webcam to kickstart the initial process of data collection and processing. Although the camera is relatively low quality without many advanced features, it was a great starting point for beginning development of the network pipeline. The first stage in our project pipeline was to develop a dataset which we could use to train our Path Prediction Network. To do this, we had the idea of leveraging the pose information by projecting future poses into our frame information. Given enough poses stamps, this would produce an accurate path for our network.

To get camera outputs, we hooked up our camera to our in-vehicle desktop and interfaced it with a simple camera based ROS node. Although we weren’t able to correct for colour distortions, we went through the standard process of intrinsic and extrinsic calibration using standard tools. Interestingly, the images had constant green hue which was a clear case of improper white balancing. Nevertheless, these images allowed us to begin building out our Pose-to-Path processing pipeline.

<p align = 'center'>
<img src = '/assets/img/vo-pose-good.gif' width = '720px'>
</p>

<p align = 'center'><i>
Wheel odometry extractered and filtered over time.
</i></p>

With the camera working, we went to the test track and collected a series of ROS bags with the camera. These ROS bags would record both “car state” information such as wheel speeds and camera images. Given these bags, our pipeline would need to pair each image with its associated pose, and then project future poses back in the images. However, the main issue was that we did not have actual pose information in our recorded ROS bags. 

<p align = 'center'>
<img src = '/assets/img/vo-pose-features.png' width = '720px'>
</p>

<p align = 'center'><i>
Example frame of Visual Odometry features..
</i></p>

To extract the actual pose, we wrote a Wheel Odometer ROS node that would take in “car state” messages with wheel speeds and numerically integrate to get wheel position overtime. As we initially expected, the odometry had significant drift. Since our pipeline only needed relative poses to certain camera images, the drift only minimally impacted the projections into the image. Nevertheless, we still tried other techniques such as trying to generate poses from a Deep Network (called DFO), and using classical Computer Vision based Pose estimation. The outputs didn’t improve our results much, thus we kept the simple wheel odometer node for our pose estimates. 
