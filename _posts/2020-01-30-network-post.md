---
layout: post
title:  "Training a Prediction Network"
date:   2020-01-30 11:22:33
author:  Caravel Team
---

After many various iterations of our  Pose-to-Path data processing pipeline, we were eventually able to get a somewhat consistent dataset which consists of RGB-Heatmap image pairs. Given the team’s experience and stability, the team select the Tensorflow framework for both the network architecture and training pipeline implementation. 

The network needed to be able to regress full-image heats-maps: meaning that given an input RGB image, the network would output an image mask of the same size which showed the general output path that should be taken along the current lane. Such a supervised image-to-image problem is quite similar to the classic problem of semantic segmentation, thus the team searched for inspiration from recent semantic segmentation models for inspiration. In particular, the network needed to be real-time to handle the dynamic nature of the lane-centering problems. For this, we used our previous experience with the state-of-the-art ICNet model, which was one of the only networks architectures that was capable of doing 30Hz inference on large images (1024x2048 resolution).

However, a standard segmentation network would not suffice. We modified the standard ICNet by:

* Randomly initializing the network instead of pre-traninig it on a classification dataset ImageNet. 
* Replaced the Classification Head with linear Regression Head to receive heatmaps instead of softmaxed class outputs.
* Updating the training pipeline to use Regression based losses.

<p align = 'center'>
<img src = '/assets/img/test-network-output.gif' width = '320px'>
</p>

<p align = 'center'><i>
Example output of the test network on a test dataset.
</i></p>

With these changes, we were able to get reasonable outputs when training and validating on images from a single data collection run. One main issue we had with this initial iteration was projecting back in into our vehicle frame from the camera frame. This would involve doing a ground plane projection, which would distort the network outputs. Thus, for a future iteration we are thinking of changing the input and out perspectives for the network.
