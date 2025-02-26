# Running jobs

## **CPU jobs**

### **Interactive CPU jobs**
You can request an interactive CPU job with the `srun` Slurm command. 
```sh
# Request 1 cpu on 1 node
srun --pty /bin/bash

# Exit from the compute node to request a new node
exit # or hit ctrl+d
```

### **Batch CPU jobs**
You can schedule a batch with the `sbatch` Slurm command which will place the job onto the job queue. The suggested workflow is to debug and get things working with `srun` and then transition into putting jobs into the queue.
Here is an example `sbatch` script:
```sh
#!/bin/bash
#SBATCH --nodes=1
#SBATCH --cpus-per-node=1
#SBATCH --time=10:00
#SBATCH --job-name=Example 

gcc --version  # prints out the gcc version.

python --version  # prints out the python version.  Replace this with a python call to whatever file.

sleep 5
```