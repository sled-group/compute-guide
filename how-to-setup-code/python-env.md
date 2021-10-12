---
layout: default
title: Python Environment
parent: How to Setup Your Code
nav_order: 1
---
# Python Environment
In order to run your job, you need a reliable way to setup your Python environment. You first need to decide on the right Python version, then pick a package management system to install dependencies.

## Python version
Generally speaking, try to pick one version behind the latest version that has been out at least for a quarter of a year. This will help you avoid all kinds of compatibility and stability problems. At the time of writing (October 12, 2021), this would be 3.8 (the latest version is 3.10, but it's only been out for about a week (October 4, 2021), so choose one version behind 3.9).

## Package management system
There are two major package management systems for Python: [pip](https://pip.pypa.io/) and [conda](https://docs.conda.io/). There are some crucial differences between them, but ultimately they both do their jobs quite well, so it really comes down to your personal preference. You can read more about your the similarities and differences between them in this [blog post](https://www.anaconda.com/blog/understanding-conda-and-pip).

## How to set it up
### pip
1. `ssh` into your login machine.
1. Clone your repository to your preferred location (somewhere in your home directory, `/scratch`, etc.).
1. Load your Python version using `module load`.
   1. `module avail` would show you all the available modules.
   1. For example, at the time of writing, `python/3.8.7` is available, so you'd issue `module load python/3.8.7`.
1. Create a virtual environment by issuing `virtualenv venv`. This will create a directory called `venv` where your virtual environment would exist.
1. Activate your virtual environment by issuing `source venv/bin/activate`.
    1. You can deactivate it by issuing `deactivate`.
1. While your virtual environment is activated, use `pip install` commands to install your desired packages.

Then, your job script should include the following commands before your main command:
```bash
module load python/3.8.7
source venv/bin/activate
```

### conda
1. `ssh` into your login machine.
1. Clone your repository to your preferred location (somewhere in your home directory, `/scratch`, etc.).
1. Load your Python version using `module load`.
    1. `module avail` would show you all the available modules.
    2. For example, at the time of writing, `python3.8-anaconda/2021.05` is available, so you'd issue `module load python3.8-anaconda/2021.05`.
2. Create a virtual environment by issuing `conda create -n <env-name>`. This will create a directory called `venv` where your virtual environment would exist.
    1. Note that if you want to use another Python version, you shouldn't load another version of conda, rather you'd load the same version of conda, and create a virtual environment with a different Python version by running `conda create -n <env-name> python=3.6`
3. Activate your virtual environment by issuing `conda activate <env-name>`.
    1. You can deactivate it by issuing `conda deactivate`.
4. While your virtual environment is activated, you can use both `conda install` or `pip install` to install your desired packages.
    1. Do be careful about conflicts if you use both `conda` and `pip`.

Then, your job script should include the following commands before your main command:
```bash
module load python3.8-anaconda/2021.05
# we need to source this script due to this issue: https://github.com/conda/conda/issues/7980
source /sw/arcts/centos7/python3.8-anaconda/2021.05/etc/profile.d/conda.sh
conda activate <env-name>
```
