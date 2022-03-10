---
layout: default
title: Whistler
nav_order: 1
parent: Whistler
description: "Add new user."
permalink: /whistler/add-new-user
---
# How to add new user to Whistler



Add them to the `/data` directory, where they should store their large files at.
```
sudo su
cd /data
mkdir <uniqname>
chown <uniqname>:<uniqname> <uniqname>
```

Tell them to set up key-pair login as opposed to password login.
