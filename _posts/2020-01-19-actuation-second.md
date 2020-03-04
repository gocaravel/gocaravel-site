---
layout: post
title:  "Longitudinal Actuation"
date:   2020-01-19 11:09:12
author:  Caravel Team
---

Longitudinal actuation of the car has been achieved! I was able to control the
acceleration and decceleration of the car, giving us full control of the
movement of the vehicle.

The key to figuring out longitudinal acceleration lies in the fact that the car
internally disables acceleration/decceleration commands unless ACC has been
manually engaged. This involves bringing the car up to 30 km/h and pressing the
ACC button on the steering wheel.

Once the ACC system has been engaged, the acceleration/decceleration commands
we were sending finally got through to the car. I was able to control the speed
of the car using a joystick just like with the steering wheel.

Thanks to the openpilot discord community for their help in resolving this
issue!.
