---
title: Goals
permalink: /docs/goals/
---

### Scope

This project is driven by the vision of a unmanned, autonomous delivery
vehicle. The vehicle would be specifically designed to carry groceries and
takeout instead of human passengers, and be equipped with the hardware
necessary to enable autonomous capabilities.

Outside of our capstone, we are part of a larger team working towards the
overarching concept of a complete vehicle. There is a subteam dedicated to
producing a hardware prototype as well as a subteam implementing software
modules enabling vehicle autonomy on a 2019 Toyota Corolla Hatchback.

However, due to the immense scope of building complete hardware and software
prototypes, **the focus of our capstone is selected to only encompass the
perception system of our software prototype**. This includes the design and
development of algorithms that use camera images to derive some understanding
of the traffic scene. This understanding is then used by the vehicle to make
decisions regarding how it behaves.

### Objectives

It is infeasible to implement complete autonomy for a vehicle in an 8 month
time-frame. Therefore, we planned to focus on enabling two core capabilities:


* **Automatic Lane Keeping:** The vehicle should be able to steer itself
  in order to stay within lane lines.
* **Adaptive Cruise Control:** The vehicle should be able to adjust its
  speed to maintain a certain distance to an obstable in front of it.

While adaptive cruise control can be accomplished by using distance sensor
inputs such as radar, automatic lane keeping relies heavily on images to
identify lane lines. Therefore, the perception algorithms we implement will be
used primarily to identify lane lines in a traffic scene.

We hope to produce a lane detection system that:

* can accurately and reliably identify lane lines in a traffic scene
* can be adapted to be used in a variety of weather and road conditions
* produces consistent output from frame to frame


