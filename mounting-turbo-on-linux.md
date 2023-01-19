---
layout: default
title: Mounting Turbo Volume on Linux Machines
nav_order: 120
description: "Guide to mount Turbo volume for new servers."
permalink: /mounting-turbo-on-linux
---
## Add linux machine to Turbo export list:

- Go to [SRS portal](https://srs.it.umich.edu/orders/services/2) and modify the Turbo volume export list by adding the new linux machine's hostname to the list.

- Go to [ARC portal](https://portal.arc.umich.edu/project/chaijy/turbo/volume-detail/coe-chaijy) to view/modify user access to the Turbo volume. It also shows current remaining disk space on the Turbo volume.

## Mount/Un-mount Turbo Volume on Linux Machines

Mount:
```
sudo mount -t nfs coe-chaijy.turbo.storage.umich.edu:/coe-chaijy /nfs/turbo/coe-chaijy
```
Un-mount:
```
umount -f -l /nfs/turbo/coe-chaijy
```

## To fix NFS UID displayed as “nobody”
Overwrite `/etc/idmapd.conf` with the following (need `sudo` to write to `/etc/idmapd.conf`):
```
[General]

Verbosity = 0
Pipefs-Directory = /run/rpc_pipefs
# set your own domain here, if it differs from FQDN minus hostname
Domain = umich.edu

[Mapping]

Nobody-User = nobody
Nobody-Group = nogroup

[Translation]
Method = nsswitch
```
Then run:
```
sudo nfsidmap -c
```

## [Optional] Change UID/GID for a user

**This is only needed if a server is not set up by DCO and thus its UIDs and GIDs for the users are not in sync with those in UMich directory.**

> ⛔️️ **WARNING**: This will break the whole file system for a user if not run properly. Make sure you know what you are doing. Be sure the change the fields with `<>` in the script with the correct information.

Tell the user to not use the computer until the followings finish.

Use a different user account to log in:

```bash
ssh <some_other_user>@<linux_machine_hostname>
sudo su
```

Log off the user whose UID/GID needs to be changed:

[https://askubuntu.com/questions/12180/logging-out-other-users-from-the-command-line](https://askubuntu.com/questions/12180/logging-out-other-users-from-the-command-line)


```bash
sudo pkill -KILL -u <username>
vim /home/<some_other_user>/change_uid_gid.sh    # modify the necessary username, UID/GID
sh /home/<some_other_user>/change_uid_gid.sh
```

Below is the `change_uid_gid.sh` script:

```bash
# put the information we need in variables

username=<uniqname>

old_uid=<old_uid>  # looks up current (old) uid

new_uid=<new_uid>

# do dangerous stuff

echo "[$(date)] Changing UID/GID for user $username from $old_uid to $new_uid" >> "$username"_change.txt

# update the user ID and group ID for $username

usermod -u $new_uid $username

groupmod -g $new_uid $username

# update the file ownerships

# NB: you cannot combine the next two chowns, or files where

# only the uid xor the gid matches won't be updated

chown -Rhc --from=$old_uid $new_uid /    # change the user IDs

chown -Rhc --from=:$old_uid :$new_uid /  # change the group IDs

setfacl -m "u:$new_uid:r-x" /media/$username

setfacl -x "u:$old_uid" /media/$username

echo "[$(date)] Finished changing UID/GID for user $username from $old_uid to $new_uid" >> "$username"_change.txt
```