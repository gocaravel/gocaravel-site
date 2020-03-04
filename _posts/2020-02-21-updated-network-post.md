---
layout: post
title:  "Prediction Network Updates"
date:   2020-02-21 1:01:45
author:  Caravel Team
---

With the updated camera and updated datasets, we decided to address the previous issue of predictions slightly degrading during from the forward facing Range View (RV) to Birds-Eye-Veiw (BEV). Such a reformulation of the network input-output encoding required as to first project the image into BEV, and then draw the poses directly into BEV. Other than getting rid of the distortions, we also hypothesized that the BEV version of the Prediction Network would actually make the prediction task easier, thus lead to better quality outputs. Once we integrated the changes, we noticed significantly better outputs shown in the below image.

<p align = 'center'>
<img src = '/assets/img/bev-network-inference.gif' width = '720px'>
</p>

<p align = 'center'><i>
Example Prediction Network output in BEV. Left is input image, middle is filtered network prediction projection  to image, right is raw network prediciton heatmap.
</i></p>

With the prediction network working somewhat well, the next task would be to collect a larger dataset for training and testing. 