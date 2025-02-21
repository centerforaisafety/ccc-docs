# Running jobs

## CPU jobs

### Interactive CPU jobs
You can request an interactive CPU job with the `srun` Slurm command. 
```sh
# Request 1 cpu on 1 node
srun --partition=cpu_only --pty /bin/bash

# Exit from the compute node to request a new node
exit # or hit ctrl+d
```

!!! Note
    If you are an undergraduate, you may need to use `--partition=single` when requesting a node.

### Batch CPU jobs
You can schedule a batch with the `sbatch` Slurm command which will place the job onto the job queue. The suggested workflow is to debug and get things working with `srun` and then transition into putting jobs into the queue.
Here is an example `sbatch` script:
```sh
#!/bin/bash
#SBATCH --nodes=1
#SBATCH --cpus-per-node=1
#SBATCH --time=10:00
#SBATCH --partition=cpu_only
#SBATCH --job-name=Example 

# Recommended way if you want to enable gcc version 10 for the "sbatch" session 
source /opt/rh/devtoolset-10/enable

gcc --version  # if you print it out again here it'll be version 10 

python --version  # prints out the python version.  Replace this with a python call to whatever file.

sleep 5
```