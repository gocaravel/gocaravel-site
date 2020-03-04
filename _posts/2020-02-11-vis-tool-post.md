---
layout: post
title:  "Visualizing Predictions"
date:   2020-02-11 10:45:49
author:  Caravel Team
---

We recently added a new feature to our stack to help with debugging and visualization. Previously, the network outputs and actuation outputs were all being visualized independently. To help with this integrated tool, we used an open source project called [streetscape.gl](https://github.com/uber/streetscape.gl) which was released by Uber. It’s a WebGL powered tool that Uber made to visualize their own autonomous vehicle sensors and outputs.

<p align = 'center'>
<img src = '/assets/img/visualization-app.png' width = '720px'>
</p>

<p align = 'center'><i>
Screenshot of the visualization tool showing perception output in blue and planner output in green.
</i></p>

The integration was a bit tricky since the tool did not support ROS, do we needed to do some modifications to their app. But in the end we were able to visualize network predictions, speed and other ROS messages.