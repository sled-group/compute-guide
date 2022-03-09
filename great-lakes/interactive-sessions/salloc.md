---
layout: default
title: salloc
parent: Interactive Sessions
nav_order: 4
---

# salloc

[`salloc`](https://slurm.schedmd.com/salloc.html) is Slurm's default way of spinning up an interactive session. It basically allocates a node, executes a command and exits. If you don't specify a command, it executes your default shell, essentially giving you an interactive session. This is probably the quickest way to spin up an interactive session. However, if you exit out of that shell, the node goes away, so it is a bit inconvenient to use than other methods.
