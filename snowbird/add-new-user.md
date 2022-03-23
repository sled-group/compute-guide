---
layout: default
title: Add New User
nav_order: 1
parent: Snowbird
description: "Add new user."
permalink: /snowbird/add-new-user
---
# How to add new user to Snowbird

Note: This guide is intended for Ph.D. students to add access for their mentees, should they require Snowbird access. Snowbird use should have human subject studies and work on SLEDBot. Remember, Snowbird access should be given on a need-to-use basis, which means users should always try if their demand can be sufficed using Great Lakes first and only use Snowbird if they have to. The Ph.D. student will be responsible for their mentees' use of Snowbird - make sure to educate mentees about best practices and responsibilities that comes with `sudo` access.

Add a new user via command line:

Snowbird has been set up by DCO and has a UMich user management system

```
sudo dcoadduser <uniqname>
```
This command will add a user to Snowbird and they can access the machine using their umich credentials.

Add the new user to have `sudo` access:
```
sudo usermod -aG sudo <uniqname>
```

<!-- 

```
sudo adduser <uniqname>
```
You will see output like this - create a temporary password, and set the full name of the user:

```
Adding user `<uniqname>' ...
Adding new group `<uniqname>' (1001) ...
Adding new user `<uniqname>' (1001) with group `<uniqname>' ...
Creating home directory `/home/<uniqname>' ...
Copying files from `/etc/skel' ...
Enter new UNIX password: 
Retype new UNIX password: 
passwd: password updated successfully
Changing the user information for <uniqname>
Enter the new value, or press ENTER for the default
    Full Name []: 
    Room Number []: 
    Work Phone []: 
    Home Phone []: 
    Other []: 
Is the information correct? [Y/n]
```

Press `Y` to confirm.

Add the new user to have `sudo` access:
```
sudo usermod -aG sudo <uniqname>
``` -->

<!-- Add them to the `/data` directory, where they should store their large files.
```
sudo su
cd /data
mkdir <uniqname>
chown <uniqname>:<uniqname> <uniqname>
```

Now give the new user their username and password (do **NOT** send this in plain text electronically!) and tell them to [change their password](https://www.cyberciti.biz/faq/change-a-user-password-in-ubuntu-linux-using-passwd/) as soon as possible.

Also tell the new user to set up key-pair access and use that to log in as soon as possible, as opposed to using password login. -->
