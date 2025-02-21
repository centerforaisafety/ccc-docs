# Running Jobs on the Cluster

All compute is managed with **SLURM**. You can run:
- **Interactive jobs** (for debugging/development)
- **Batch jobs** (for longer or large-scale runs)

## Interactive Sessions
Use `srun`:
```sh
# 1 CPU core
srun --pty bash

# 1 GPU
srun --gres=gpu:1 --pty bash
```