---
layout: post
title:  "Lateral Actuation"
date:   2020-01-17 11:09:12
author:  Caravel Team
---

We were able to get lateral actuation on the car. It was quite an arduous process!
Here's a video of me steering the car with a joystick:

![Joystick Actuation](/assets/img/actuation.gif)

To accomplish actuation, a
[comma.ai panda](https://comma.ai/shop/products/panda-obd-ii-dongle) was
installed on the Toyota Corolla. This device intercepts the CAN bus of the car,
allowing us to read the data being passed around in the car's internal systems
and also allows us to send custom commands to the car's steering assist and
cruise control systems.

The first step was getting a CAN readout from the panda - this involved
flashing the device with the latest firmware and making sure that it had the
right settings to be compatible with the car. Next, comma.ai's
[openpilot](https://github.com/commaai/openpilot) and
[openpilot-tools](https://github.com/commaai/openpilot-tools) repositories were
instrumental in figuring out how to interface with the panda. Since some of the
openpilot libraries were needed to communicate with the panda, I had to
integrate the openpilot repository into our build system, which was a huge
hassle. Once I was able to read CAN data from the car, I wrote a basic CAN
interface module to read and update  the car state at 100 Hz. This would
provide knowledge of the car's steering angle, speed, and other useful data to
the rest of our system.

The next hurdle was trying to send custom commands to the CAN bus in order to
actuate the car. In order to create an easy testing environment I created a
small script to read input from a joystick and translate that to steering and
acceleration commands to send to the car.

At first, I could only control the HUD of the car, but after some digging I
realized that the panda had an internal permissions system that enabled and
disabled commands based on the "safety model" that was set. After setting the
appropriate safety model, I was finally able to control the steering wheel.
Unfortunately, the acceleration is still unresponsive.
