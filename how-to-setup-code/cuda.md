---
layout: default
title: CUDA
parent: How to Setup CUDA
nav_order: 2
---
# CUDA
There are two instances of CUDA libraries when you use PyTorch. One is the one that comes packaged with the PyTorch package itself, and the other is the system-wide CUDA installation. PyTorch would use the one that's packaged with it, while other libraries would most likely choose to use the system-wide installation. Most of the time, you don't need to worry about this as both installations of CUDA are the same version (10.2 at the time of writing October, 2021), but things get tricky when they go out of sync.

These two versions can go out of sync when you try to use the new NVIDIA A40 GPUs. At the time of writing (October, 2021), PyTorch depends on CUDA 10.2 by default, but NVIDIA A40 GPUs require CUDA 11. As a result, your vanilla PyTorch code will thrown an error about the incompatibility. This is easily fixed by running the appropriate installation commands provided in the official PyTorch website, but this only upgrades the CUDA installation that's packaged with PyTorch. So, if you use another library that uses CUDA, it'll use the system-wide installation, which by default is 10.2, and complain. Thankfully, this is easily fixed by loading the right module by issuing the command `module load cuda/11.4.0`.
