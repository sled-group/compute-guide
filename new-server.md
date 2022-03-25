---
layout: default
title: Set Up New Server (For Administrators)
nav_order: 100
description: "Guide to set up new server at SLED Research Group."
permalink: /new-server
---
# Set Up New Server (For Administrators)

## Naming Convention
At SLED lab, we name our servers after [ski resorts](https://www.skiresort.info/ski-resorts/usa/) to honor the "SLED" snowsport spirit! Use single word if possible (e.g. for "Beaver Creek", do "sled-beavercreek"). Check if it is available on [EECS Hostname Check](https://www.eecs.umich.edu/dco/tools/hostcheck/).

## DCO Setup
Email UMich DCO staff Jamie Goldsmith (jlgoldsm@umich.edu) and Laura Fink (laura@umich.edu) to request a DCO set up for the new server. Give them the hostname (e.g. "sled-beavercreek.eecs.umich.edu") that you came up with in the previous step. UMich DCO will help set up the machine including registering its MAC address (so that it gets Internet access), adding their public key to `root` access (so that they can maintain it when needed) and adding directory service (so that users can use their UMich username and password to log in when system admin add them via `dcoadduser`), etc.

## Install TigerVNC

Install `xfce`:
```
sudo apt install xfce4 xfce4-goodies
```
We are ready to install the TigerVNC Server and its dependencies.
```
sudo apt install tigervnc-standalone-server tigervnc-common
```
