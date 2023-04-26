---
layout: default
title: Storage
nav_order: 20
parent: Great Lakes
description: "About File System on GreatLakes"
has_children: true
---

# Storage

There are 4 types of file systems you can use on Great Lakes, listed in decreasing order of speed: `/scratch`, `/home`, Turbo and Data Den. The trade-off for speed is permanence of data. This means we should start with `/scratch` then go down the list based on your archival needs.

`/scratch` is by far the fastest, but your data will be purged if not accessed for 60 days. We also get 10TB of `/scratch` per root account, i.e., our entire lab, which means `/scratch` should really be your default choice for most of your work, especially disk I/O heavy work like data preprocessing, data reading, checkpointing, etc.

`/home`, while not as fast as `/scratch`, does give you permanence. However, there is a per-user limit of 80GB. Appropriate data to store here would be code and other development artifacts like pip or conda caches, which are stored in your `/home` directory by default.

Turbo is slower than `/home` as it is an nfs, but it gets automatically backed up every day. We as a lab pay for 20TB as of 4/21/2023, but we can't use the full 20TB as some of it has to be reserved for backup snapshots. Turbo is appropriate for fairly static data that needs ready access, such as data sets or pretrained weights. _Turbo is **NOT** the choice for your code or other development artifacts!!!_ Storing this type of data on Turbo will not only cause your program to run slower, but also inconvenience others by taking up unnecessary space. It's generally OK to read in data sets or pretrained weights directly from Turbo especially if you're going to read them once keep them in memory throughout the lifetime of your program. However, it'd be significantly faster if you copy over your data to `/scratch` from Turbo if your program is going to read it constantly from disk, e.g., reading an image or video data set. Also, it's not wise to write to Turbo constantly as it'll be a bottleneck. For example, if you're downloading a huge data set, it's better to download it first to `/scratch` then `rsync` over to Turbo.

Data Den is the slowest of them all, and it's appropriate for long-term archival of data that don't need ready access. We get 100TB for free as a lab. We currently use Data Den to back up data that used to be owned by students who have graduated.

## References

- [Great Lakes User Guide](https://arc.umich.edu/greatlakes/user-guide/)
- [Great Lakes Policies](https://arc.umich.edu/document/greatlakes-policies/)
- [Turbo FAQ](https://arc.umich.edu/turbo-faq/)
- [Data Den](https://arc.umich.edu/data-den/)
- [Resource Management Portal](https://portal.arc.umich.edu/project/chaijy/great-lakes/root-account-detail/chaijy_root)
