---
layout: default
title: Install VirtualGL+TurboVNC to Enable 3D Acceleration for Remote Access
nav_order: 110
description: "Guide to install VirtualGL+TurboVNC for new servers."
permalink: /virtualgl-installation
---
# Background Knowledge

[Understanding what X server is](https://www.youtube.com/playlist?list=PLXEcKYHTGBdQqfmIiyw6KueAFExDGVQbx)

[Understanding what VirtualGL is](https://virtualgl.org/About/Background)

# Part A: TurboVNC + VirtualGL Installation Guide

### Uninstall Current VNC (*TurboVNC* for example): 

```
dpkg -r turbovnc
```

*Reference: https://virtualgl.org/vgldoc/2_1_3/#hd005006*


### Uninstall Nvidia-*:

```
sudo apt-get remove --purge '^nvidia-.*'
```

- `nvidia-smi` to check whether nvidia driver has been uninstalled

### Install VirtualGL:

Follow the [Reference Link](https://rawcdn.githack.com/VirtualGL/virtualgl/3.0/doc/index.html#hd005001)


### Install Nvidia-driver

Follow the [Reference Video](https://www.youtube.com/watch?v=FAknvXs4M1w)



### Disable "HardDPMS" in xorg.conf:

```
sudo nvidia-xconfig -a --allow-empty-initial-configuration
```

```
sudo vim /etc/X11/xorg.conf
```

Delete all lines about "DPMS"

Add `Option "HardDPMS" "false"` to the bottom of all monitor, device and screen sections (**within those section blocks**)

*Reference: https://virtualgl.org/Documentation/HeadlessNV*

- Issue about "HardDPMS": 
    - Read More: https://groups.google.com/g/virtualgl-users/c/d8k1ujwKJXo



### VirtualGL Configuration:

Follow the [Reference Link](https://rawcdn.githack.com/VirtualGL/virtualgl/3.0/doc/index.html#hd006)

##### Tips:
- Make sure you successfully shut down the display manager of your computer
- In *option 1 (Configure server for use with VirtualGL (GLX + EGL back ends))* : Select **"No"** for all those three questions 


### TurboVNC Installation:

```dpkg -i turbovnc*.deb```

*Reference: https://virtualgl.org/vgldoc/2_1_3/#hd005001*


### Final Check:
Open one terminal:
```
watch -n 0.2 nvidia-smi 
```

Open another terminal:
```
vglrun glxgears
```

Make sure a new process using GPU called ***glxgears*** appear in the first terminal.



# Part B: GPU Access on a remote Linux server in ThreeDWorld

[Install TDW on a remote Linux server](https://github.com/threedworld-mit/tdw/blob/master/Documentation/lessons/setup/install.md#install-tdw-on-a-remote-linux-server)

#### Comments:
- For /etc/X11/xorg.conf, **no need to** remove ServerLayout and Screen section
- **No need to** run x-server by `sudo nohup Xorg :<Display server name> -config /etc/X11/xorg.conf & `

#### TDW Run:
- Download [the latest build of TDW](https://github.com/threedworld-mit/tdw/releases/latest/) and extract the zip file into **TDW**
- Create Python script. Make sure to set *launch_build=False* to Controller
- In one shell window, run the controller: 

  ```
  python3 my_controller.py
  ```

- In the second shell window, `cd` to **TDW**, the location of the build (`TDW.x86.64`)

  ```
  vglrun ./TDW.x86_64 -port=1071
  ```

