---
layout: default
title: Slurm Accounts
nav_order: 2
description: "Guide to using the right Slurm accounts"
permalink: /slurm-accounts
---

# Slurm Accounts

There are a few different Slurm accounts you can use at SLED depending on your research needs.

- `chaijy0`: This account is funded through the [University of Michigan Research Computing Package (RCP)](https://arc.umich.edu/umrcp/). We applied for this while waiting for our nodes with NVIDIA A40 GPUs to arrive in the fall of 2021. This will give you nodes with NVIDIA V100 GPUs. Expect some queuing time as the nodes are shared with other labs. This does cost money (it gets taken out of the RCP funding we got), so be mindful when using it.
- `chaijy1`: You shouldn't use this account unless you know what you're doing. This account is directly funded by Dr. Chai, and gives you nodes with NVIDIA V100 GPUs (same pool as `chaijy0`). Expect some queuing time and be extra careful with using this as Dr. Chai gets charged.
- `chaijy2`: This account is associated with the two A40 GPU nodes we as a lab have purchased. As a result, we don't get charged for using this account, and there's almost no wait time unless someone from SLED is using them. This should be your primary account. There is some cost sharing where if someone from another lab needs more nodes than they own, they can dip into our nodes and we'd get credited for that. We can use these credits to dip into other nodes we don't own.
- `engin1`: This is a free account provided by ARC for debugging purposes. It gives you nodes with NVIDIA V100 GPUs. Try to use this account for interactive sessions or testing out your scripts. It's shared across the whole College of Engineering, so technically you may need to wait for your jobs to launch, but usually there isn't much wait.
