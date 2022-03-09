---
layout: default
title: Setting Time Limit for Your Job
parent: Job Management
nav_order: 2
---
# Setting Time Limit for Your Job

Job execution time is a limited resource, so Slurm requires that every job has an associated time limit for efficient scheduling. The default time limit is 60 minutes for Great Lakes, but you can change it by using the `--time` option. For example, in your job script, you'd do something like the following:

```bash
#!/bin/bash

# time format is D-HH:MM:SS
# other formats are acceptable, but use this to keep things simple.
# time limit is 1 day, 12 hours, 30 minutes and 45 seconds
#SBATCH --time=1-12:30:45
```

You can of course set this option directly with `sbatch`.
```bash
# time format is D-HH:MM:SS
# other formats are acceptable, but use this to keep things simple.
# time limit is 1 day, 12 hours, 30 minutes and 45 seconds
$ sbatch --time=1-12:30:45
```

Now, there are two catches: 1. you can't change the time limit of a running job, 2. if you ask for a lot of time, you might have to wait longer for your job to run. So, it's a balancing act of requesting enough time for your job to run, but not too much so your job gets executed quickly.

## Tips on setting the right time limit
### Have a good estimate on your job running time
There are many ways you can do this. The simplest would be to run your job for a couple of epochs, measure the time and use that to extrapolate the total running time. Then, submit a new job with the estimated total running time with a bit of padding.

### (Advanced) Use the special Slurm signal
Say your wait time is too long because your estimated running time is too high. Or you just want to make your job to be more resilient against time limits. Then you can tell Slurm to signal your job before it's about to run out of time by setting the `--signal` option and handle things more gracefully by handling that signal. For example, if your job script contains the following:

```bash
#SBATCH --signal=USR1@90
```

Slurm will send a `SIGUSR1` to your job 90 seconds before it runs out of time. Now it's just a matter of writing the code to handle it gracefully. One way is to save a checkpoint, requeue the job (`scontrol requeue <job-id>`), restore the checkpoint and resume the training. If you use [PyTorch Lightning](https://pytorch-lightning.readthedocs.io/), this is already taken care for you.
