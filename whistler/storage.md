---
layout: default
title: Storage
nav_order: 2
parent: Whistler
description: "About file storage on Whistler."
permalink: /whistler/storage
---
# Storage

Whistler comes with three 4TB SSD disks. The first is mounted at `/` (the root directory), the second is mounted at `/home` and the third is mounted at `/data`. The first is intended to be used for the Ubuntu system, the second for home directories; the third is intended to be used for large file storage.

You should store large files like datasets and training checkpoints under `/data/<uniqname>`.
