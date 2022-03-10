---
layout: default
title: Storage
nav_order: 2
parent: Whistler
description: "About file storage on Whistler."
permalink: /whistler/storage
---
# Storage

Whistler comes with two 3.8TB SSD disks. The first is mounted at `/` (the root directory) and the second is mounted at `/data/`. The first is intended to be used for the Ubuntu system and home directories; the second is intended to be used for large file storage.

You should store large files like datasets and training checkpoints under `/data/<uniqname>`.
