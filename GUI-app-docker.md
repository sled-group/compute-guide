---
layout: default
title: Running GUI applications in Docker
nav_order: 125
has_children: false
description: "Running GUI application in Docker and connect to it via VNC."
permalink: /docker-display-vnc
---

# Running GUI application in Docker and connect to it via VNC

## Connect via VNC to the host machine

## Copying the Cookie to connect X Server Displays
```
xauth list
```
This will output something like this:

```
sled-whistler.eecs.umich.edu:2  MIT-MAGIC-COOKIE-1  45db54b7cf77e29b0cda77136ef651d6
sled-whistler/unix:2  MIT-MAGIC-COOKIE-1  45db54b7cf77e29b0cda77136ef651d6
sled-whistler.eecs.umich.edu:7  MIT-MAGIC-COOKIE-1  83637cf2079edf78f2d1d351bf039191
sled-whistler/unix:7  MIT-MAGIC-COOKIE-1  83637cf2079edf78f2d1d351bf039191
sled-whistler.eecs.umich.edu:8  MIT-MAGIC-COOKIE-1  f932fcc437e8abc29f0802d539433e41
sled-whistler/unix:8  MIT-MAGIC-COOKIE-1  f932fcc437e8abc29f0802d539433e41
sled-whistler.eecs.umich.edu:9  MIT-MAGIC-COOKIE-1  7f8b16bd4bd358d4263f450147130e5e
sled-whistler/unix:9  MIT-MAGIC-COOKIE-1  7f8b16bd4bd358d4263f450147130e5e
sled-whistler.eecs.umich.edu:10  MIT-MAGIC-COOKIE-1  3123ea326b75354ce36cbad68a94e931
sled-whistler/unix:10  MIT-MAGIC-COOKIE-1  3123ea326b75354ce36cbad68a94e931
sled-whistler.eecs.umich.edu:12  MIT-MAGIC-COOKIE-1  0e0b885f314f0398b0a9228399a17385
sled-whistler/unix:12  MIT-MAGIC-COOKIE-1  0e0b885f314f0398b0a9228399a17385
```

Copy the line `sled-whistler/unix:<i>  MIT-MAGIC-COOKIE-1  <cookie value>` which is the cookie of coresponding display of your vncserver. `<i>` is the index of your VNC session.


## Create a container with nvidia runtime and display
```
docker run -it --gpus "device=1" --net=host -e DISPLAY=:<i> -v /tmp/.X11-unix/:/tmp/.X11-unix  <REPOSITORY:TAG>
```

## Add the cookie in the container

In the container, use this command to add the X Server Display
```
xauth add <cookie>
```

Check the list to verify if the cookie is successfully added
```
xauth list
```
The output should be:

```
root@sled-whistler:/# xauth list
sled-whistler/unix:<i>  MIT-MAGIC-COOKIE-1  <cookie value>
```

Check the X Server Display
```
echo $DISPLAY
```

The output should be:
```
root@sled-whistler:/# echo $DISPLAY
:<i>
```
## Verification

Run `glxgears` in the Docker container, 
```
glxgears
```
if glxgears isn't available inside docker,install it with
```
sudo apt install mesa-utils
```
You should now see a gears window running in VNC. If everything runs fine, you can now start the GUI application you need in the Docker.
