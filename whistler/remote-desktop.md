---
layout: default
title: Remote Desktop (GUI)
nav_order: 3
parent: Whistler
description: "Remote Desktop."
permalink: /whistler/remote-desktop
---
# Remote Desktop/GUI Access to Whistler

## Configure VNC (Only need to do this one time)
`TigerVNC`, which is a VNC server program, has been installed on Whistler. All we need to do is to modify `~/.vnc/xstartup`.

First, if `~/.vnc/xstartup` already exists, back it up by moving it:
```
mv ~/.vnc/xstartup ~/.vnc/xstartup.bak
```

If it does not exist, create it and set its permission:

```
cd ~
mkdir .vnc
cd .vnc
touch xstartup
chmod 700 xstartup
```
Then add the following lines to it (via `nano` or `vim`):
```
#!/bin/sh
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
startxfce4 &

[ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup
[ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
xsetroot -solid grey
vncconfig -iconic &
```

This tells the VNC server to use `xfce` as its desktop (GUI) provider as opposed to the default gnome desktop. This is because gnome desktop does not seem to support multiple simoutaneous VNC sessions for one user; it also occasionally freezes and becomes non-responding.

## Start VNC session

Each time you need to access remote desktop, you need to start a VNC session first via:

```
vncserver
```

(The first time you run this, it will ask you to set a password for VNC. Just set the password and remember it. If you need to change the password later, use `vncpasswd`.)

This will output something like this:
```
Warning: sled-whistler.eecs.umich.edu:1 is taken because of /tmp/.X1-lock
Remove this file if there is no X server sled-whistler.eecs.umich.edu:1

New 'sled-whistler.eecs.umich.edu:2 (<uniqname>)' desktop at :2 on machine sled-whistler.eecs.umich.edu

Starting applications specified in /home/<uniqname>/.vnc/xstartup
Log file is /home/<uniqname>/.vnc/sled-whistler.eecs.umich.edu:2.log

Use xtigervncviewer -SecurityTypes VncAuth -passwd /home/<uniqname>/.vnc/passwd :2 to connect to the VNC server.
```

Note the `:2` above - it starts from `:2` because `:1` has been taken. This means this new VNC session was started at `5902` port. VNC uses ports starting from `5901`. So `:1` will spawn at `5901`; `:2` will spawn at `5902` and so on.

Now the VNC server is up and running!

## Connect to a VNC session
First, we need to establish an SSH tunneling to forward the `5902` port to our own computer and then connect via `localhost`. To establish the SSH tunnel (on Campus Wi-Fi or UMich VPN), on your laptop:
```
ssh -L 59000:localhost:5902 -C -N -l <uniqname> sled-whistler.eecs.umich.edu
```
The command will hang there and keep running - this is fine.

Or off-VPN through jump machine:
```
ssh -J <uniqname>@login.itd.umich.edu  -L 59000:localhost:5902 -C -N -l <uniqname> sled-whistler.eecs.umich.edu
```

Then, on your laptop, open your favorite VNC client. For macOS users, the Finder already has a built-in VNC tool: `Go > Connect to Server`. (Btw, I recommend checkout `RealVNC` client for Mac users - it seems to be faster.)

To connect:
- Host: localhost
- Port: 59000

For macOS for example, enter `vnc://localhost:59000` and hit 'Connect'.

You will be asked to enter the password you set for VNC.

Then you should be entering the desktop (GUI).


## Kill a VNC session

To show active VNC sessions:
```
vncserver -list
```
Look up the session number you want to terminate, e.g. `:3`.

To end a VNC session (e.g. `:3`), on Whistler:
```
vncserver -kill :3
```
