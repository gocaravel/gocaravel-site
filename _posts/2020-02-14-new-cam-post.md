---
layout: post
title:  "Updating Our Camera and Datasets"
date:   2020-02-14 2:05:06
author:  Caravel Team
---

After any weeks of testing and iterating with a basic webcam, we obtained a full featured camera capable of various features that would help improve the system. In particular, we were sent the 2.3 MP Triton Lucid Camera which captured at a `1920x1200px` resolution. Although the camera was of high quality, we noticed right away the need to modify our existing software and hardware stack to support it. In particular, the camera required an additional power source. Thus, our first step was to get a PoE+ card and install it in the desktop. Then, we designed and 3D printed a camera mount to use in the vehicle. With the hardware being complete, we began the software support by calibrating the camera. 

<p align = 'center'>
<img src = '/assets/img/camera-and-mount.jpg' width = '720px'>
</p>

<p align = 'center'><i>
Triton camera with added mount for the vehicle.
</i></p>

Surprisingly, the extrinsic calibration was quite difficult. Depending on the yaw, roll and pitch, the transformation we had for our network would vary quite significantly. After some iteration, we were able converge at somewhat suitable values. Next was the ROS node and camera interface, which was also a challenge. The camera interface was quite low level, but after some tweaking we were able to enable the following features during images capture:

* Real-time frame capture by disabling the internal camera queue.
* Hardware `Binning` to reduce the image resolution from `1920x1200px` to `960x600px`.
* Enabling `AutoWhiteBalance` to get rid of the previous green hue we had with our Webcam.
* Enabling `AutoExposure`, if we were to get a dataset over various days, we would ideally want the brightness of all the images to be similar to not confuse the network. 

<p align = 'center'>
<img src = '/assets/img/snow-bag-example.gif' width = '720px'>
</p>

<p align = 'center'><i>
Example dataset collected with updated camera and capture node.
</i></p>

With these changes, we recollect a dataset along a road. The images were clearly much better and certainly would improve the network. 
