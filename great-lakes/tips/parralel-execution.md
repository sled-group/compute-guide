---
layout: default
title: To really utilize the multi cores in GL
parent: Tips
grand_parent: Great Lakes
nav_order: 1
---
# Choose the correct library
Two major choice for simple parallel execution in Python are
- multiprocessing Library
- jobslib Library

However, ```jobslib``` does not seem to work on GL. Instead, it utilizes only a single core no matter how many cores you have.

Thus, it is highly suggested to use the ```multiprocessing``` Lib.

When using it, sometimes you need to run the following commands at the start of your code to correctly evoke multi cores.
``` python3
core_mask_op = "taskset -pc %s %d" % ('0-40', os.getpid())
os.system(core_mask_op)
```
- Replace ```40``` there with ```num of CPUs -1```

# Check if everything's fine
Run ```top``` in CLI to check the CPU usage.
