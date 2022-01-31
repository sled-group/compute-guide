---
layout: default
title: Slurm Accounts
nav_order: 2
description: "Guide to using the right Slurm accounts"
permalink: /slurm-accounts
---

# Slurm Accounts

There are a few different Slurm accounts you can use at SLED depending on your research needs.

- `chaijy0`: This account is funded through the [University of Michigan Research Computing Package (RCP)](https://arc.umich.edu/umrcp/), and provides access to nodes with NVIDIA V100 GPUs. Here, we’re given 80,000 free CPU hours which are replenished annually in July, so we should use it as much as possible.
    - Expect some queuing time as the nodes are shared with other labs.
    - Unless otherwise noted, this should be your default choice when selecting an account. An announcement will be made in Slack if/when we are out of credit on this account, in which case you should use `chaijy2`.
- `chaijy1`: This account is directly funded by Dr. Chai's research grants, and provides access to nodes with NVIDIA V100 GPUs (same pool as `chaijy0`). 
    - ***Only PhD students have permission to use this account, and it should be avoided unless given permission by Dr. Chai.***
    - Expect some queuing time as the nodes are shared with other labs.
- `chaijy2`: This account is associated with the two exclusive A40 GPU nodes we purchased as a lab. We have a large balance of free usage here which is enough to fund 5 years of GPU time for each of our 16 A40 GPUs (this covers their entire life on Great Lakes).
    - When chaijy0 has long wait times or the GPU memory is insufficient, use this account instead.
    - To request A40 GPUs on this account, use the partition `spgpu` instead of `gpu`. If these GPUs have a long queue time, you can also use the account credit to request V100 GPUs on the general `gpu` partition.
    - While we only own 16 GPUs, our lab may use a total of 20 GPUs at one time on this account, as the nodes are part of a small cluster shared with a few other faculty members' labs. As we are unlikely to fully utilize our nodes at all times (and thus build up extra credit), it's okay to use more GPUs than we own during deadlines and peak work times.
- `engin1`: This is a free account provided by ARC for debugging purposes. It gives you nodes with NVIDIA V100 GPUs. Try to use this account for interactive sessions or testing out your scripts. It's shared across the whole College of Engineering, so technically you may need to wait for your jobs to launch, but usually there isn't much wait.

**To avoid any accidental charges to the wrong account, make sure you carefully specify the billing account on all jobs.** You can do this either in the [header of your Slurm job script](https://arc.umich.edu/greatlakes/slurm-user-guide/), or under “Job Options” in the [Great Lakes Job Composer](https://greatlakes.arc-ts.umich.edu/pun/sys/myjobs).

**If you need to be added to any of SLED’s Great Lakes accounts, please contact Shane Storks.** Most of us should be granted access to chaijy0 and chaijy2 upon joining SLED, but it’s possible some members have been missed. We’ll be trying to keep the list of users up to date.

**To check usage limits and account membership,** take a look at the [ITS portal](https://portal.arc.umich.edu/projects).
