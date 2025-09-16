---
layout: post
title:  "Track Timer"
description: "Track timers cost a lot of money, so I made one"
image: /assets/images/track-timer-finished.jpg
date:   2025-07-23
---
## General Overview
I ran track in highschool, and I absolutely loved it. I mostly ran the 100m and 200m, and shaving down time is a very strong motivator for me. I looked for an affordable timing system, but what I need ranges from a few hundred dollars to several thousands. I then decided it would be a fun project to make one myself.

In many track events, such as the 400m, 800m, 1600m, you start the race in about the same spot you finish, because they are multiples of 400m. Creating a fully automatic timing (FAT) system is fairly simple for these events. Simply have a single device with a buzzer, a timer, and some way to detect crossing the finish line. However, events like the 100m, 200m, or 300m hurdles, you start quite far away from the finish line. Some problems arise when timing these events. 

Sound travels quite slow, taking about 0.29 seconds to travel 100m. This means that the start gun must be very close to the runner. This means that we need two devices, and they need near-instant communication. FAT systems generally solve this with a very long cable, which is reliable, but expensive. The other solution is wireless communication. I did some research, and decided the nRF24L01 paired with some Arduino Nanos would be a good solution. 

For detecting the finish line, I went with a TF-Luna LiDAR sensor. It is perhaps a bit more accurate than I need, but it works well for my needs. 

I first assembled this on breadboards, soldered them to perfboard (I got the perfboard at a conference for free from a scrap bin, its weirdly shaped and I have no idea what its original purpose was) then moved it to a 3D printed case that I designed.

### Hardware
- Arduino Nano (USB Type-C)
- TF-Luna LiDAR sensor
- nRF24L01+PA+LNA
- nRF24L01 breakout adapter for the 3.3V regulator
- 0.91 inch OLED Display Modules
- Piezo buzzer
