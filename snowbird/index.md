---
layout: default
title: Snowbird
has_children: true
nav_order: 4
description: "This is a guide to using the Snowbird workstation at SLED Reserch Group."
permalink: /snowbird
---
# Guide to Using Snowbird

To access (on UMich VPN or campus Wi-Fi):
```
ssh <uniquname>@sled-snowbird.eecs.umich.edu
```
Or, if you are off-campus and don't want to use VPN, you can also do:
```
ssh -J <uniqname>@login.itd.umich.edu <uniquname>@sled-snowbird.eecs.umich.edu
```

![Snowbird](/compute-guide/snowbird/snowbird.jpg)

Snowbird is a lab-owned server sitting in BBB 2912. It has the following hardware:

- **CPU**: Intel Xeon Silver 4216 @ 32x 3.2GHz
- **Memory**: 64GB
- **GPU**: NVIDIA RTX A4000
- **Disk**: 1TB SSD + 4TB HDD
<!-- - **Network**: 10 Gbps dual port -->
- **System**: Ubuntu 18.04 **DO NOT UPGRADE**
<!-- - **Power Supply**: 1300w -->

The intention of this compute is to help with tasks that is not doable on Great Lakes such as:
- Human subject data collection
- Developing software in ROS to use on our PAL TIAGo SLEDBot

For these reasons, all users are given `sudo` access on Snowbird. Remember, with great `sudo` power comes great responsibility. Be responsible and know what you are doing before doing it!

All Ph.D. students in the lab has been added as a user. For SLED mentees who need access to Snowbird, please ask your mentor to add you as a user following [guide to adding new user](/compute-guide/snowbird/add-new-user).
