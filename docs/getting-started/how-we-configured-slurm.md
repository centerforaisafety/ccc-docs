# Slurm

## How we configured Slurm
The priority of your jobs in the SLURM queue is determined based on the size of the job, the time you’ve been waiting and your group’s previous usage relative to other groups (“fair share”, in SLURM’s terminology).

You should aim to request the minimum number of GPUs needed to run your job efficiently. Requesting more GPUs than needed will result in your group’s priority declining faster than otherwise, which means you will need to wait longer in the queue to run jobs in future. You can check the utilisation of GPU cores and memory to see if jobs are running efficiently using:
```sh
srun –jobid= nvidia-smi
```
We have configured Slurm for sending email and slack notifications for various job stages (begin, fail, requeue, complete, etc) from the `do-not-reply@safe.ai` email address (check spam). See the cluster documentation for further details. You can add notifications to your job by adding the following lines to your SBATCH file: 
```sh
#SBATCH –mail-user=mailto:{email},slack:{slack-member-id} 
#SBATCH –mail-type=ALL
```
!!! Warning "Please do not do any work on the login node. This includes installing things (request a CPU node to do so)."