---
layout: default
title: Add New User
nav_order: 1
parent: Whistler
description: "Add new user."
permalink: /whistler/add-new-user
---
# How to add new user to Whistler

Note: This guide is intended for Ph.D. students to add access for their mentees, should they require Whistler access. Remember, Whistler access should be given on a need-to-use basis, which means users should always try if their demand can be sufficed using Great Lakes first and only use Whistler if they have to. The Ph.D. student will be responsible for their mentees' use of Whistler - make sure to educate mentees about best practices and responsibilities that comes with `sudo` access.

Add a new user via command line:

Whistler has been set up by DCO and has a UMich user management system

```
sudo dcoadduser <uniqname>
```
This command will add a user to Whistler and they can access the machine using their umich credentials.

Add the new user to have `sudo` access:
```
sudo usermod -aG sudo <uniqname>
```

Add them to the `/data` directory, where they should store their large files.
```
sudo su
cd /data
mkdir <uniqname>
chown <uniqname>:<uniqname> <uniqname>
```

Now give the new user their username and password (do **NOT** send this in plain text electronically!) and tell them to [change their password](https://www.cyberciti.biz/faq/change-a-user-password-in-ubuntu-linux-using-passwd/) as soon as possible.

Also tell the new user to set up key-pair access and use that to log in as soon as possible, as opposed to using password login.
