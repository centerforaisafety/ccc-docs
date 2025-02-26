# Running jobs

## **What is Slurm?**

The CAIS Compute Cluster uses [Slurm](https://slurm.schedmd.com/), an open-source resource manager and job scheduler, used by many of the world's [supercomputers and computer clusters](https://top500.org/).

Slurm supports a variety of job submission techniques. By accurately requesting the resources you need, you’ll be able to get your work done.


## **Slurm commands**
Slurm allows requesting resources and submitting jobs in a variety of ways. The main Slurm commands to submit jobs are listed in the table below:

| Command  | Description | Behavior |
| -------- | ----------- | -------- |
| `salloc` | Request resources and allocates them to a job | Starts a new shell, but does not execute anything |
| `srun`   | Request resources and runs a command on the allocated compute node(s) | Blocking command: will not return until the job ends |
| `sbatch` | Request resources and runs a script on the allocated compute node(s) | Asynchronous command: will return as soon as the job is submitted |

## **How we configured Slurm**
The priority of your jobs in the Slurm queue is determined based on the size of the job, the time you’ve been waiting and your group’s previous usage relative to other groups (“fair share”, in Slurm’s terminology).

You should aim to request the minimum number of GPUs needed to run your job efficiently. Requesting more GPUs than needed will result in your group’s priority declining faster than otherwise, which means you will need to wait longer in the queue to run jobs in future. You can check the utilisation of GPU cores and memory to see if jobs are running efficiently using:
```sh
srun --jobid=<JOBID> nvidia-smi
```