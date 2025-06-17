---
layout: default
title: Storage
nav_order: 2
parent: Snowbird
description: "About file storage on Snowbird."
permalink: /snowbird/storage
---
# Storage

Snowbird comes with one 1TB SSD mounted at `/` (the root directory), one 2TB SSD mounted at `/home` and one 4TB SSD disks mounted at `/data`. The first is intended to be used for the Ubuntu system, second for home directories; the third is intended to be used for large file storage.

You should store large files like datasets and training checkpoints under `/data/<uniqname>`.
