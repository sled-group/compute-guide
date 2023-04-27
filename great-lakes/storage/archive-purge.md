---
layout: default
title: Archive and Purge
parent: Storage
grand_parent: Great Lakes
nav_order: 1
---

# Archive and Purge

Storage has gotten cheaper, but it is not free, e.g., [Turbo](turbo.md), so we should be diligent about archiving and purging. Generally, when a student leaves a lab, e.g., graduation, we should either archive their data on [Data Den](data-den.md) or completely purge them.

Furthermore, we can archive or purge data that have not been accessed for a while. You can use [GUFI](https://github.com/umich-arc/gufi-archive) to get data on this. This typically takes a long time, so it's a good idea to run it as a Slurm job. Here's an example Slurm script that runs GUFI on Turbo.

```bash
#!/bin/bash

### DO NOT USE GPU NODES!
#SBATCH --partition=standard
#SBATCH --time=02-00:00:00
#SBATCH --job-name=gufi
#SBATCH --mail-user=<your-email@umich.edu>
#SBATCH --mail-type=BEGIN,END
### Totally fine to use chaijy0
#SBATCH --account=chaijy0
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=1
#SBATCH --cpus-per-task=8
#SBATCH --mem-per-cpu=16GB
#SBATCH --output=/home/%u/%x-%j.log

module load singularity
singularity exec gufi_master.sif gufi_dir2index -n 8 /nfs/turbo/coe-chaijy/ /scratch/chaijy_root/chaijy0/<uniqname>/GUFI
```

Once this is done, you can run various reporting commands:

**summary.sh**

```bash
#!/bin/bash

### DO NOT USE GPU NODES!
#SBATCH --partition=standard
#SBATCH --time=02-00:00:00
#SBATCH --job-name=gufi-summary
#SBATCH --mail-user=<your-email@umich.edu>
#SBATCH --mail-type=BEGIN,END
### Totally fine to use chaijy0
#SBATCH --account=chaijy0
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=1
#SBATCH --cpus-per-task=8
#SBATCH --mem-per-cpu=16GB
#SBATCH --output=/home/%u/%x-%j.log

module load singularity
singularity exec --bind /etc/passwd gufi_master.sif summary.sh /scratch/chaijy_root/chaijy0/<uniqname>/GUFI/coe-chaijy/ 180
```

**dirsum.sh**

```bash
#!/bin/bash

### DO NOT USE GPU NODES!
#SBATCH --partition=standard
#SBATCH --time=02-00:00:00
#SBATCH --job-name=gufi-dirsum
#SBATCH --mail-user=<your-email@umich.edu>
#SBATCH --mail-type=BEGIN,END
### Totally fine to use chaijy0
#SBATCH --account=chaijy0
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=1
#SBATCH --cpus-per-task=1
#SBATCH --mem-per-cpu=2GB
#SBATCH --output=/home/%u/gufi-dirsum/%x-%j.log

module load singularity

# Define the array of directory names
DIR_NAMES=('dir1' 'dir2')

# Run the command in parallel for each directory in the array
for DIR_NAME in "${DIR_NAMES[@]}"; do
  # Create a folder for the parallel job
  mkdir -p /home/<uniqname>/gufi-dirsum/$DIR_NAME

  salloc -N1 -n1 --cpus-per-task=4 --mem-per-cpu=16GB --account=chaijy0 \
         srun --chdir=/home/<uniqname>/gufi-dirsum/$DIR_NAME --output=/home/<uniqname>/gufi-dirsum/$DIR_NAME/${DIR_NAME}-%j.log \
              singularity exec --bind /etc/passwd gufi_master.sif dirsum.sh /scratch/chaijy_root/chaijy0/<uniqname>/GUFI/coe-chaijy/$DIR_NAME 180 &
done

# Wait for all parallel tasks to complete
wait
```

Once you've determined which data to archive, you can use `archivetar` to do so. See [Data Den](data-den.md) for more details.
