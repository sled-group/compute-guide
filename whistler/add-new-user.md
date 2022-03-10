---
layout: default
title: Add New User
nav_order: 1
parent: Whistler
description: "Add new user."
permalink: /whistler/add-new-user
---
# How to add new user to Whistler

Add the user via command line:
```
sudo adduser <uniqname>
```
You will see output like this - just create a temporary password, and set the full name of the user:

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

Add the user to have `sudo` access:
```
sudo usermod -aG sudo <uniqname>
```

Add them to the `/data` directory, where they should store their large files at.
```
sudo su
cd /data
mkdir <uniqname>
chown <uniqname>:<uniqname> <uniqname>
```

Now give the new user their username and password (do NOT send this in plain text electronically!) and tell them to [change their password](https://www.cyberciti.biz/faq/change-a-user-password-in-ubuntu-linux-using-passwd/) as soon as possible.

Also tell the new user to set up key-pair login and use that to login as soon as possible, as opposed to password login.
