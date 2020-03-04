---
layout: post
title:  "Heatmap Label Generation for Prediction Network"
date:   2020-01-22 5:28:16
author:  Caravel Team
---

Once we collected the initial ROS Bags and augmented them with our Pose(generated from wheel odometry), we needed to implement the process of projecting future poses back into our images. With such a tool working, we would ideally be able to automatically label images with paths simply by driving through an environment. The idea was that when these image-paths were used to train a network, we would have a model capable of predicting paths. Thus, our Path Prediction Network.

<p align = 'center'>
<img src = '/assets/img/initial-dataset.gif' width = '720px'>
</p>

<p align = 'center'><i>
Left shows the image frame with superimposed pose data. Right shows the generated heatmap for training.
</i></p>
Our implementation consisted of us looping through images, projecting the future posses and then finally applying a gaussian filter along the height of the image to generate a heat map. Such a heat map would represent variance for the actual centreline path the vehicle could take - something which is compatible with a neural network. In the next post, we plan on going over the basics of the initial network implementation.
