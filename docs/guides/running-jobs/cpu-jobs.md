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

## **Submit the job**
Once your batch script is ready, you can submit it to the scheduler with:
```sh
$ sbatch cpu_job.sh
Submitted batch job 123456
```
Upon success, `sbatch` will return the ID it has assigned to the job (in this example, `123456`)

## **Check the job**
After submission, your job will enter the queue in the `PENDING` state. When resources become available and your job has sufficient priority, it will start running (`RUNNING` state). If it completes successfully, it will transition to `COMPLETED`. Otherwise, it may show `FAILED` or another terminal state.

Use `squeue` to check the status of your job:
```sh
$ squeue -u $USER
     JOBID   PARTITION    NAME      USER ST   TIME  NODES NODELIST(REASON)
    123456     compute Example <username> R    0:12    1   compute-permanent-node-535
```

## **Slurm output file**
By default, Slurm writes any output from your script to a file named slurm-<job-id>.out. You can list the contents of that output file as follows (using the same job ID that was returned by `sbatch`):
```sh
$ cat slurm-123456.out
gcc (GCC) 9.4.0
Python 3.12.2
```

You can customize the output file name by addin gdirectives (e.g., `#SBATCH --output=myjob.out`) in your `sbatch` script or specifying them at the command line.