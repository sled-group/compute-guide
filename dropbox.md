---
layout: default
title: DropBox
has_children: false
nav_order: 130
description: "This is a guide to using SLED Research Group DropBox team folder."
permalink: /dropbox
---
# About DropBox Team Folder
SLED has a [DropBox Team Folder](https://www.dropbox.com/home/ENGIN-SLED-Research-Data) linked to the `sled-group` [MCommunity group](https://mcommunity.umich.edu/group/SLED%20Research%20Group). It is meant for long-term storage of *de-identified human subjects data* collected during IRB regulated research projects.

# FAQ

## Why DropBox instead of something else?
DropBox is an ideal solution for storage of this type of data for several reasons:
1. It’s more secure than our lab servers, e.g., [Whistler](../whistler/index.md) or [Snowbird](../snowbird/index.md), which aren’t backed up.
2. Access control is easy, and partly automated by being connected to our MCommunity group.
    a. In some cases, approval/permission may be required to share collected data outside of UMich. As such, we want to avoid storing human subjects data in places where SLED alums or external collaborators may have access, e.g., Google Drive, lab servers.
    b. **You are responsible for knowing the access restrictions stipulated by your IRB and enforcing them through DropBox permissions.**
3. Storage is unlimited and it can be easily mounted to your file system.
    a. **Before mounting or syncing data to another device, ensure that this is permissible under your IRB.**
4. It’s centralized and has a convenient web interface, so it will be easy to keep track of data from different projects as students come and go.

## What if my data is identifiable?
In this case, you likely have stronger IRB restrictions on managing your data. One possible approach is to temporarily store data on one of our lab servers in a folder encrypted with [EncFS](https://manpages.ubuntu.com/manpages/xenial/man1/encfs.1.html) until it is de-identified. If de-identification is not possible (extremely unlikely in our work), you may need to consider other options, e.g., purchasing a specialized [Turbo drive](https://arc.umich.edu/turbo/).
