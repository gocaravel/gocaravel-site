---
layout: post
title:  "Rejecting Outliers"
date:   2020-03-03 10:20:02
author:  Caravel Team
---

Up until now, we postprocess the network outputs by simply fitting a polynomial
to the pixels that have a positive detection above some threshold, weighted by
the network output for each pixel. We then assume that this polynomial is
representative of the path future path of the car, or a lane line in the case
of LaneNet.

However, the problem with this method is that our net outputs are not very
consistent. Oftentimes there are also quite a few false detections that
affect the polyline fitting. Coupled with the fact that the polyline does
not extrapolate well past observed data points, the result is that the path
detection can fluctuate quite wildly on a frame-by-frame basis and that
it will not represent the ground truth well at times.

<p align = 'center'>
<img src = '/assets/img/pre_tracking.gif' width = '256px'>
</p>

<p align = 'center'><i>
Raw polyline fitting of Lanenet detections for the right lane line.
The green regions show the pixels that the network deemed above a
certain probability to be the right lane line. The line gradient
represents the polyline that was fit to the network outputs.
</i></p>

To address the problem of false detections, we needed a fast outlier rejection
algorithm. An obvious candidate was RANSAC, but unfortunately RANSAC was too
slow. We decided to implement our own outlier rejection algorithm based on
classical computer vision methods.

Our algorithm first applied a threshold to the network output, then used
connected components to create blobs of positive detections. We would then
select the blob that was most likely to be the correct detection based on
hand-crafted heuristics, such as blob area and shape.

This improved the final polyline when multiple prominent detections were
present, but temporal consistency is still a big issue. When the network
outputs are not ideal, the fitted polyline will vary wildly from frame to
frame.

<p align = 'center'>
<img src = '/assets/img/post_filter.gif' width = '256'>
</p>

<p align = 'center'><i>

Polyline fitting with outlier rejection of Lanenet detections for the right
lane line.  The green regions show the pixels that have passed the outlier
rejection algorithm. Note how much less pixels are used compared to the raw
polyline fit.

</i></p>

Towards the end of the sequence, the polyline completely fits to the
more prominent detections for the center lane line. This is not desirable
behaviour for the overal system but is valid based on our heuristics.

We hope to come up with a temporal consistency method that will address
these issues.
