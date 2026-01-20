# Running jobs

## **GPU jobs**

### **Interactive GPU jobs**

Available partitions - similar to cpu partition
- cais
- schmidt_sciences
- tamper_resistance

You can request an interactive GPU job with the `srun` Slurm command.
```sh
# Request 1 GPU on 1 node (2 CPU cores are allocated per GPU by default)
srun --partition=cais --gpus=1 --pty /bin/bash
srun --partition=cais --gres=gpu:1 --pty /bin/bash # also works

# schmidt_sciences partition
srun --partition=schmidt_sciences --gpus=1 --pty /bin/bash
srun --partition=schmidt_sciences --gres=gpu:1 --pty /bin/bash

# tamper_resistance partition
srun --partition=tamper_resistance --gpus=1 --pty /bin/bash
srun --partition=tamper_resistance --gres=gpu:1 --pty /bin/bash


# Exit from the compute node to request a new node
exit  # or hit ctrl+d
```

### **Batch GPU jobs**
You can schedule a batch GPU job with the sbatch Slurm command, which will queue your job for execution on an available GPU node. As with CPU jobs, we suggest debugging your job interactively (using srun) before submitting a batch job.
Here is an example sbatch script for a GPU job:
```sh
#!/bin/bash
#SBATCH --partition=<your-partition>
#SBATCH --nodes=1
#SBATCH --cpus-per-task=2  # 2 CPUs per GPU (default ratio)
#SBATCH --gpus=1
#SBATCH --time=10:00
#SBATCH --job-name=GPU_Example

# Check that the GPU is available
nvidia-smi

# Run your GPU-accelerated application
python --version  # Replace this with your actual GPU-enabled command

sleep 5
```

Once the script is written, you can submit it to the scheduler with the `sbatch` command. Upon success, `sbatch` will return the ID it has assigned to the job
```sh
$ <username>@cais-login-0:~$ sbatch gpu_job.sh 
Submitted batch job 186269
```

### **Check the job** 
Once submitted, the job enters the queue in the PENDING state. When resources become available and the job has sufficient priority, an allocation is created for it and it moves to the RUNNING state. If the job completes correctly, it goes to the COMPLETED state, otherwise, its state is set to FAILED.

You'll be able to check the status of your job and follow its evolution with the `squeue -u $USER` command:

```sh
$ <username>@cais-login-0:~$ squeue -u $USER
     JOBID PARTITION     NAME          USER        ST   TIME    NODES  NODELIST(REASON)
      123    compute     GPU_Example   <username>  R    0:12    1      compute-permanent-node-535
The scheduler will automatically create an output file that will contain the result of the commands run in the script file. That output file is names slurm-<jobid>.out by default, but can be customized via submission options. In the above example, you can list the contents of that output file with the following commands:

$ <username>@cais-login-0:~$ cat slurm-186269.out
Tue Feb 25 23:06:42 2025       
+-----------------------------------------------------------------------------------------+
| NVIDIA-SMI 550.144.03             Driver Version: 550.144.03     CUDA Version: 12.4     |
|-----------------------------------------+------------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id          Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |           Memory-Usage | GPU-Util  Compute M. |
|                                         |                        |               MIG M. |
|=========================================+========================+======================|
|   0  NVIDIA A100-SXM4-80GB          On  |   00000000:91:00.0 Off |                    0 |
| N/A   36C    P0             85W /  400W |       1MiB /  81920MiB |      0%      Default |
|                                         |                        |             Disabled |
+-----------------------------------------+------------------------+----------------------+
                                                                                         
+-----------------------------------------------------------------------------------------+
| Processes:                                                                              |
|  GPU   GI   CI        PID   Type   Process name                              GPU Memory |
|        ID   ID                                                               Usage      |
|=========================================================================================|
|  No running processes found                                                             |
+-----------------------------------------------------------------------------------------+
Python 3.12.2
```
