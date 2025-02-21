# Cluster Overview

The CAIS Compute Cluster consists of **32 GPU nodes** (Oracle Cloud bare-metal servers), each with:

| Feature                 | Description                                                                             |
| ----------------------- | --------------------------------------------------------------------------------------- |
| **GPU Nodes**           | 32 GPU nodes (Oracle Cloud bare-metal), each with 8× NVIDIA A100 80GB GPUs (total 256)  |
| **CPU Cores**           | Dual 64-core AMD CPUs per node (total 4096 CPU cores across the cluster)                |
| **Local NVMe SSD**      | 27.2 TB per node (870 TB total system storage)                                          |
| **RDMA Network**        | 1,600 Gbit/sec total, providing high-bandwidth and low-latency inter-node communication |
| **Operating System**    | Ubuntu 22.04                                                                            |

The cluster is managed using Ansible and Terraform. The cluster uses **SLURM** for job scheduling, with **WekaFS** for the shared distributed parallel filesystem.

This powerful setup enables large-scale AI/ML experiments that would be costly or cumbersome elsewhere. Services are provided free of charge for approved AI safety projects.