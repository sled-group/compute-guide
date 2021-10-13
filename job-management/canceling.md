---
layout: default
title: Canceling Your Job
parent: Job Management
nav_order: 1
---
# Canceling Your Job
You can always simply use the web interface to stop your job, but a better way is to write your script to catch SIGINT and gracefully stop itself. You can either catch it in your bash script, or in your Python script.

You can issue a SIGINT, or any kind of signal for that matter, to a job by using `scancel`. Make sure to use the `--full` option, otherwise the top-level bash script does not get the signal. You can read more about this behavior in this [discussion](https://bugs.schedmd.com/show_bug.cgi?id=9715).

```bash
# notice it's INT not SIGINT. Other signals work the same way, e.g. KILL not SIGKILL
scancel --full --signal=INT <job-id>
```
