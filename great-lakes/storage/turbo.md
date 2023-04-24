---
layout: default
title: Turbo
parent: Storage
grand_parent: Great Lakes
nav_order: 1
---

# Turbo

[Turbo](https://arc.umich.edu/turbo/turbo-user-guide/) is a high-capacity, reliable, secure, and fast storage solution. It is slower than `/scratch` or `/home`, but the data on Turbo are periodically backed up and won't be purged. Turbo is appropriate for fairly static data that needs ready access, such as data sets or pretrained weights. _Turbo is **NOT** the choice for your code or other development artifacts!!!_

You can access Turbo on a Great Lakes node at `/nfs/turbo/coe-chiajy`. Since it's an nfs, it can be mounted on other servers, such as your personal desktop. The detailed instructions can be found [here](https://arc.umich.edu/turbo/turbo-user-guide/#document-2).

## Performance Considerations

Turbo is an nfs, which is not the fastest filesystem. As mentioned before, it is slower than `/scratch` or `/home`. This means that directly reading from or writing to Turbo a handful of times in your script is totally fine, but if you find yourself doing so constantly, you may see a significant drop in your throughput at some point. The workaround is to use `/scratch` or `/home` instead. For example, if you want to download a huge dataset, e.g., EGO4D, it's better to download it to `/scratch`, then use `rsync` to copy over to Turbo. If you want to read in a huge image dataset stored in Turbo, it's better to copy that over to `/scratch` and read from there.

## File Permissions

Unlike `/scratch` or `/home`, Turbo is a _shared_ storage system, so it's important to set appropriate file permissions on your data. By default, Turbo sets the owner of the data to be you, the group owner to be `coe-chaijy-turbo`, and sets the permission bits to be `770` or `rwxrwx---`. This means that the owner and a group member (of which you are) can read, write and execute, but others can do neither. If you're not familiar with the file permissions, you can read this [tutorial](https://www.tutorialspoint.com/unix/unix-file-permission.htm). This [unix permissions calculator](https://wintelguy.com/permissions-calc.pl) is very useful too.

### Setting Permissions for Private Data

If you want to store some private data on Turbo, first ask yourself if Turbo is really where you want to store them. Again, Turbo is a _shared_ storage system and we generally want to store data that need to be shared with the whole lab. If you think Turbo is indeed the place to store them, then you can set the permission bits to `600` (`rw-------`) (or `700` (`rwx------`) for directories), which would only allow the owner, which is you, to read and write. If you want lab members to be able to read the file, you'd set `640` (`rw-r-----`) (or `750` (`rwxr-x---`) for directories). If you also want others to be able to read the file, you'd set `644` (`rw-r--r--`) (or `755` (`rwxr-xr-x`) for directories).

### File Permissions When Accessing Turbo Outside of Great Lakes

Turbo by default uses the user and group IDs managed by ARC. This means that if you create a file on a system with different user and group IDs such as Whistler, the ownership of files gets a bit wonky. Let's work through an example to understand what happens.

First, let's create a file from a Great Lakes node:

```bash
# Great Lakes node
$ touch /nfs/turbo/coe-chaijy/hello
$ ll /nfs/turbo/coe-chaijy/hello
-rwxrwx--- 1 kpyu coe-chaijy-turbo 0 Apr 24 11:52 /nfs/turbo/coe-chaijy/hello
```

So far so good, the owner of the file is me (`kpyu`) and the group is `coe-chaijy-turbo`.

Now, let's see how this looks on Whistler:

```bash
# Whistler
$ ll /nfs/turbo/coe-chaijy/hello
-rwxrwx--- 1 kpyu coe-chaijy-turbo 0 Apr 24 11:52 /nfs/turbo/coe-chaijy/hello
```

Looks good again! How about the reverse? Let's create a file from Whistler

```bash
# Whistler
$ touch /nfs/turbo/coe-chaijy/hello
$ ll /nfs/turbo/coe-chaijy/hello
-rwxrwx--- 1 nobody coe-chaijy-turbo 0 Apr 24 12:03 /nfs/turbo/coe-chaijy/hello
```

Huh? Who is `nobody`? Let's check it out on a Great Lakes node:

```bash
$ ll /nfs/turbo/coe-chaijy/hello
-rwxrwx--- 1 nobody coe-chaijy-turbo 0 Apr 24 12:03 /nfs/turbo/coe-chaijy/hello
```

`nobody` again. So what happened?

Remember that Whistler's users are not managed by ARC, so it has a different user ID space:

```bash
# Whistler
$ id -u kpyu
1002
# Great Lakes
$ id -u kpyu
114234337
```

So, Turbo doesn't know about user ID 1002, so it just assigns `nobody`, which is a special user that owns no files or directories. Note that the group is not affected by this, because our Turbo volume is set up so that all the files and directories inherit the permissions and group from the root `/nfs/turbo/coe-chaijy` via a mechanism called the group sticky bit.

If you try the same exercise on Snowbird, whose users are managed by ARC, you get the correct behavior:

```bash
# Snowbird
$ id -u kpyu
114234337
$ touch /nfs/turbo/coe-chaijy/hello
$ ls -l /nfs/turbo/coe-chaijy/hello
-rwxrwx--- 1 kpyu coe-chaijy-turbo 0 Apr 24 12:11 /nfs/turbo/coe-chaijy/hello

# Great Lakes
$ id -u kpyu
114234337
$ ll /nfs/turbo/coe-chaijy/hello
-rwxrwx--- 1 kpyu coe-chaijy-turbo 0 Apr 24 12:11 /nfs/turbo/coe-chaijy/hello
```
