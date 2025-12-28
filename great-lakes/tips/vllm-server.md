---
layout: default
title: Host VLLM Server on Great Lakes
parent: Tips
grand_parent: Great Lakes
nav_order: 1
---

When your research requires intensive or sustained use of large language models, it may be beneficial to temporarily host a vLLM server on Great Lakes. This approach helps reduce contention caused by multiple users independently loading and serving the same model on shared resources. One example is that multiple users would like to use Qwen model for inference, then they can share the same server to avoid the contention.

**Important note:** Hosting a vLLM server on Great Lakes is intended only for short-term use (e.g., a few days). The server will be shut down after the usage period, and the allocation should be coordinated with lab members in advance to ensure that it does not negatively impact others’ compute availability. The billing should also be considered.

# Host a vLLM Server on Great Lakes

To host a vLLM server on Great Lakes, you need to:

1. Create a virtual environment for vLLM. We recommend using `conda`, as `uv` is currently unstable for vLLM on Great Lakes.
2. Download the model weights to the shared directory: `/nfs/turbo/coe-chaijy-unreplicated/pre-trained-weights/`. This ensures consistency and avoids redundant downloads across users.
3. Submit a Slurm job to host the vLLM server. Make sure you record the hostname of the compute node assigned to your job. 
   > **Note:** This guide assumes a single-node setup, which is sufficient for most inference workloads. Multi-node configurations are not covered here.
   
   You can obtain the hostname in one of the following ways:
   * Run `hostname` directly on the node.
   * Use `squeue` while the job is running.

   Example:
   ```bash
   $ squeue -A chaijy0
       JOBID PARTITION     NAME     USER  ACCOUNT ST       TIME  NODES NODELIST(REASON)
       38987150     spgpu vllm-ser    roihn  chaijy0  R    4:19:10      1 gl1509
   ```
   In this example, the hostname is:
   ```
   gl1509.arc-ts.umich.edu
   ```

4. Create an SSH tunnel to forward traffic from a local or lab server to the compute node hosting the vLLM server. We recommend running this command from one of the **lab servers** (e.g., *whistler*, *aspen*) so that other lab members can access the service.

   ```bash
   ssh -J <uniqname>@login.itd.umich.edu -N -f \
       -L <local_port>:<gl_host_name>:<gl_vllm_port> \
       <uniqname>@greatlakes.arc-ts.umich.edu
   ```
   **Parameters:**
   * `<uniqname>`: Your UMich uniqname
   * `<local_port>`: Port on the local or lab server
   * `<gl_host_name>`: Compute node hostname (e.g., `gl1509.arc-ts.umich.edu`)
   * `<gl_vllm_port>`: vLLM server port on the node (default: `8000`)
   
   **Flags:**
   * `-N`: Do not execute a remote command
   * `-f`: Run the SSH tunnel in the background
       * If omitted, the terminal must remain open to keep the tunnel alive
   * `-L`: Enable local port forwarding
   
   
   To terminate the tunnel, first identify the process using the local port:
   ```bash
   lsof -i :<local_port>
   ```
   Example:
   ```bash
   $ lsof -i :22003
   COMMAND    PID  USER   FD   TYPE   DEVICE SIZE/OFF NODE NAME
   ssh     263790 roihn    4u  IPv6 62792077      0t0  TCP ip6-localhost:22003 (LISTEN)
   ssh     263790 roihn    5u  IPv4 62792078      0t0  TCP localhost:22003 (LISTEN)
   ```
   Then terminate the process:
   ```bash
   kill <PID>
   ```
   If you do not use `-f` when creating the ssh tunnel, you can also use `Ctrl+C` to terminate the process.

5. Verify the connection. To confirm that the tunnel is working, run a test script on the local or lab server using:

   * **Host:** `localhost`
   * **Port:** `<local_port>`

   If the connection is successful, the script should communicate directly with the vLLM server running on the Great Lakes ompute node.
