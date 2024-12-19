---
layout: default
title: Onboarding For PhD students
has_children: false
nav_order: 140
description: "Onboarding guide for new PhD students."
permalink: /Onboarding
---
# Onboarding guide for new PhD students

Welcome to SLED lab! To assist you with the onboarding process, here is a checklist to guide you:

- [ ] Lab Access
- [ ] Compute Resource Access
- [ ] Google Drive Access
- [ ] Group Github Access
- [ ] General Tips
- [ ] More ongoing ...

## Lab Access

Our laboratory has exclusive access to a dedicated lab room, located in **BBB 2912**. This space is primarily used for offline human data collection, robotics experiments, meetings, and other related activities.

The lab is equipped with several fancy devices and tools, including but not limited to:
- Tiago robot (a humanoid-like robot with one robotics arm and wheel base)
- HoloLens 2 (for Augmented Reality (AR))
- Various kitchen utensils and simulated fruits/food

Each Ph.D. student in the lab is entitled to one physical key for accessing the room. Please contact Joyce to obtain the key. Additionally, a shared key is available at 4909 BBB, primarily for use by your mentees. If you would like to use the shared key, please sign the form posted on the wall nearby. Be sure to record who is using the key and when it is being used.

## Compute Resource Access

We have several compute resources available in our lab. They can be broadly categorized into two groups: local machines and cluster servers.

1. **Local Machines:**
    We currently have four physical machines in our lab: Whistler, Aspen, Snowbird, and Baisoara. Each machine is equipped with a monitor for local access, but most usage scenarios will involve remote access. These machines differ in their intended use cases and hardware specifications:

    - **[Whistler:](https://sled-group.github.io/compute-guide/whistler)** 
        - Spec: Linux OS with two RTX A6000 GPUs.
        - Usage: Primarily for development and local test runs. Can also host demo platforms to showcase your work.
        - Location: Lab, 2nd floor.

    - **[Aspen:](https://sled-group.github.io/compute-guide/aspen)**
        - Spec & Usage: Similar specifications and usage as Whistler.
        - Location: Office, 4th floor (BBB 4909).

    - **[Snowbird:](https://sled-group.github.io/compute-guide/snowbird)**
        - Spec: Linux OS with one RTX A4000 GPU.
        - Usage: Primarily for robot-related experiments and human-centered studies. Not intended for compute-heavy workloads.
        - Location: Lab, 2nd floor.

    - **Baisoara:**
        - Spec: Windows OS.
        - Usage: Specialized for software that runs only on Windows (e.g., HoloLens applications).
        - Location: Lab, 2nd floor.
        - Important Note: Only one user can access Baisoara at a time. Although remote access is allowed, in-person users typically have priority. It is recommended to inquire beforehand if someone is currently using the machine remotely before initiating your session.
    
    
    **How to create your account?** You need to separately create an account for each physical machine, and only the existing sudo users on the machine can create the account for you. (Note: For Baisoara, you may automatically gain access by logging in with your username and password in person for the first time.) If you need help creating your account, please ask any senior Ph.D. student in our lab. You will use your UM email address and password to log in.

2. **Cluster Servers:**
    The Great Lakes Slurm cluster is a computing cluster which is the main computing resource you will be using for your research at the University of Michigan. If you would like to have the access to the great lakes cluster, you need to first follow the instructions [here](https://its.umich.edu/advanced-research-computing/high-performance-computing/great-lakes/getting-started) and then ask our senior Ph.D. students to add you into our lab's account. Check [this section](https://sled-group.github.io/compute-guide/great-lakes) for more details.


## SLED Google Drive

We maintain several shared Google Drives for the lab. To gain access, please reach out to any senior Ph.D. student who can add you to the appropriate drives.


## SLED github

We have a group [github account](https://github.com/sled-group) where we open source our codes. Please reach out to senior Ph.D. students to add you as a member.



## General Tips
1. You are free to use the lab space, including the fridge, microwave, and other shared facilities, but please keep the area tidy and clean.
2. Whistler and Aspen Usage: These machines are frequently used and often have ongoing demo processes. When running your own code, ensure that you do not interfere with existing processes, especially those utilizing the GPU. You can use `top` and `nvidia-smi` to monitor CPU/GPU usage, and set the `CUDA_VISIBLE_DEVICES` environment variable to choose which GPU to use.
3. Mentee Access and Responsibilities: You may add your mentees to the compute resources, but you are fully responsible for training them to use these resources properly. In the event that you or your mentees cause an issue with the local machines (e.g., upgrading shared utilities without authorization, causing crashes), you are responsible for restoring them to normal operation.
4. Rebooting Local Machines: If you need to reboot a local machine, inform all users at least one day in advance via the `#compute` channel so they can pause and save their work beforehand.
5. GPU Usage on Great Lakes: Due to limited GPU availability, the total GPU usage per Ph.D. student (including their mentees) must not exceed 12 GPUs. If you need to temporarily exceed this limit for up to 4 hours, send a brief notice in the `#compute` channel. Other members may request that you reduce usage back to 12 GPUs. During less busy times (e.g., summer), this rule may be relaxed, and scheduling will be managed through Slurm.
6. `ondemand` Jobs on Great Lakes: You can use `ondemand` jobs for test-runs on Great Lakes with a GUI or an interactive environment (e.g., Jupyter notebooks, VNC desktop). However, please keep `ondemand` jobs under 8 hours since they do not automatically close. It’s unlikely you will be continuously working for more than 8 hours, and leaving jobs running longer than necessary may block resources.