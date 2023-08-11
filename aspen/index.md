---
layout: default
title: Aspen
has_children: true
nav_order: 4
description: "This is a guide to using the Aspen workstation at SLED Reserch Group."
permalink: /aspen
---
# Guide to Using Aspen

To access (on UMich VPN or campus Wi-Fi):
```
ssh <uniquname>@sled-aspen.eecs.umich.edu
```
Or, if you are off-campus and don't want to use VPN, you can also do:
```
ssh -J <uniqname>@login.itd.umich.edu <uniquname>@sled-aspen.eecs.umich.edu
```

![Aspen](/compute-guide/aspen/aspen.jpg)

Aspen is a lab-owned server sitting in BBB 2912. It has the following hardware:

- **CPU**: AMD Ryzen Threadripper PRO 5955WX (4.0GHz, 16 cores, 64MB cache, DDR4- 3200, 280W)
- **Memory**: 256GB DDR4 3200MHz 
- **GPU**: 2x Nvidia Quadro RTX A6000 48GB
- **Disk**: 3.84TB NVMe SSD (M.2, PCIe Gen 4, 1DWPD) (boot `/` drive) + 15.36TB Data center NVMe SSD (2.5", PCIe Gen 4, 1DWPD) (`/data` drive)
- **Network**: 10 Gbps dual port
- **System**: Ubuntu 22.04 LTS
- **Power Supply**: 1600w

The intention of this compute is to help with tasks that is not doable on Great Lakes such as:
- Machine learning development
- Deadline-sensitive tasks

Note:
- This workstation does not have a monitor or keyboard. We don't intend to add one due to space constraints in our 2nd floor lab. Please use SSH to access the workstation.
- Because this machine will handle deadline-sensitive tasks which need the machine to be reliably running, we will reserve `sudo` access only to PhD students. For mentees who needs to install software, please ask your mentor to install it for you.
