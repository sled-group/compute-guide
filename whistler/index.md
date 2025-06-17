---
layout: default
title: Whistler
has_children: true
nav_order: 3
description: "This is a guide to using the Whistler workstation at SLED Reserch Group."
permalink: /whistler
---
# Guide to Using Whistler

To access (on UMich VPN or campus Wi-Fi):
```
ssh <uniquname>@sled-whistler.eecs.umich.edu
```
Or, if you are off-campus and don't want to use VPN, you can also do:
```
ssh -J <uniqname>@login.itd.umich.edu <uniquname>@sled-whistler.eecs.umich.edu
```

![Whistler](/compute-guide/whistler/whistler.jpg)

Whistler is a lab-owned server sitting in BBB 2912. It has the following hardware:

- **CPU**: Intel Core i9-10900X (10 physical cores, 20 threads, 3.7GHz, Liquid Cooling)
- **Memory**: 256GB DDR4 3200MHz 
- **GPU**: 2x Nvidia Quadro RTX A6000 48GB
- **Disk**: 3x 4TB SSD
- **Network**: 10 Gbps dual port
- **System**: Ubuntu 20.04 **DO NOT UPGRADE**
- **Power Supply**: 1300w

The intention of this compute is to help with tasks that is not doable on Great Lakes such as:
- Interactive rendering that requires a physical display
- Programs that have special dependencies which cannot be installed on Great Lakes

For these reasons, all users are given `sudo` access on Whistler. Remember, with great `sudo` power comes great responsibility. Be responsible and know what you are doing before doing it!

All Ph.D. students in the lab has been added as a user. For SLED mentees who need access to Whistler, please ask your mentor to add you as a user following [guide to adding new user](/compute-guide/whistler/add-new-user).
