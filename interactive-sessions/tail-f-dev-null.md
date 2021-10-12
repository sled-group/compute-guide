---
layout: default
title: `tail -f /dev/null`
parent: Interactive Sessions
nav_order: 3
---
# `tail -f /dev/null` Trick
Sometimes you want to quickly launch a node and `ssh` into it instead of launching a whole JupyterLab session or remote desktop. In that case, you can put `tail -f /dev/null` as the last command of your job, which will prevent the job from exiting without eating up CPU cycles. For example, your job script might be something like:

```bash
#!/bin/bash
echo $SLURMD_NODENAME
tail -f /dev/null
```
Then, either use the web interface or inspect the `$SLURMD_NODENAME` environment variable to figure out the node name and simply `ssh` into it from your login machine.
