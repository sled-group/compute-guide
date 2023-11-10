---
layout: default
title: Slurm Accounts
nav_order: 2
parent: Great Lakes
description: "Guide to using the right Slurm accounts"
permalink: /great-lakes/slurm-accounts
---

# Slurm Accounts

There are a few different Slurm accounts you can use at SLED depending on your research needs. Regardless of funding source, each account provides access to nodes with CPU cores only (on the `standard` partition), NVIDIA V100 GPUs (on the `gpu` partition), and NVIDIA A40 GPUs (on the `spgpu` partition). You can see [here](https://arc.umich.edu/greatlakes/configuration/) for specific information about the available hardware on Great Lakes. 

Read below to determine which account to use:

- `chaijy0`: This account is funded through the [University of Michigan Research Computing Package (RCP)](https://arc.umich.edu/umrcp/). Here, we’re given 80,000 free CPU hours which are replenished annually in July, so we should use it as much as possible.
    - Unless otherwise noted, this should be your default choice when selecting an account. An announcement will be made in Slack if/when we are out of credit on this account, in which case you should use `chaijy2`.
    - Expect some queuing time as the nodes are shared with other labs.
- `chaijy1`: This account is directly funded by Dr. Chai's research grants, and provides access to nodes with NVIDIA V100 GPUs (same pool as `chaijy0`). 
    - ***Only PhD students have permission to use this account, and it should be avoided unless given permission by Dr. Chai.***
    - Expect some queuing time as the nodes are shared with other labs.
- `chaijy2`: This account is funded from our lab's purchase of two exclusive A40 GPU nodes. We have a large balance of free usage here which is enough to fund 5 years of GPU time for each of our 16 A40 GPUs (this covers their entire life on Great Lakes).
    - When chaijy0 has long wait times, use this account instead.
    - While we only own 16 GPUs, our lab may use a total of 20 GPUs at one time on this account, as the nodes are part of a small cluster shared with a few other faculty members' labs. As we are unlikely to fully utilize our nodes at all times (and thus build up extra credit), it's okay to use more GPUs than we own during deadlines and peak work times.
- `engin1`: This is a free account provided by ARC for debugging purposes. You can use this account for interactive sessions or testing out your scripts, but you should limit your usage as much as possible as it is monitored by ARC. It's shared across the whole College of Engineering, so technically you may need to wait for your jobs to launch, but usually there isn't much wait.

**To avoid any accidental charges to the wrong account, make sure you carefully specify the billing account on all jobs.** You can do this either in the [header of your Slurm job script](https://arc.umich.edu/greatlakes/slurm-user-guide/), or under “Job Options” in the [Great Lakes Job Composer](https://greatlakes.arc-ts.umich.edu/pun/sys/myjobs).

**If you need to be added to any of SLED’s Great Lakes accounts, please contact any of SLED's PhD students.** Most of us should be granted access to chaijy0 and chaijy2 upon joining SLED, but it’s possible some members have been missed. We’ll be trying to keep the list of users up to date.

**To check usage limits and account membership,** take a look at the [ITS portal](https://portal.arc.umich.edu/projects). To add or remove membership: manage through the [ITS portal](https://portal.arc.umich.edu/projects).
