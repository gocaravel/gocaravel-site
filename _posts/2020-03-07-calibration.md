---
layout: post
title:  "Re-calibrating our camera"
date:   2020-03-07 10:20:02
author:  Caravel Team
---

Once the path for the car is detected in image space, it needs to be
transformed into world space coordinates so that it can be used by the planner
module. Intrinsic and extrinsic camera calibration is required to perform
this transformation.

We recently changed the camera settings and positioning in order to get
better image quality. We therefore had to re-calibrate our camera to
reflect its updated configuration.


<p align = 'center'>
<img src = '/assets/img/calib1.jpg' width = '600'>
</p>

<p align = 'center'>
<img src = '/assets/img/calib2.jpg' width = '600'>
</p>

<p align = 'center'><i>
Oles calibrating camera intrinsics with a checkerboard.
</i></p>



<p align = 'center'>
<img src = '/assets/img/ext_calib.png' width = '600'>
</p>

<p align = 'center'><i>
Visualization of the camera's extrinsic calibration.
</i></p>
