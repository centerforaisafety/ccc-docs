# CAIS Compute Cluster

Welcome to the documentation for the **Center for AI Safety (CAIS) Compute Cluster**, a GPU-accelerated research cluster for Artifical Intelligence/Machine Learning (AI/ML) safety research maintained by the Center for AI Safety. On this site we provide guidance on accessing and using the cluster, from basic usage to advanced workflows.

If you have questions not answered here, please consult the [FAQ](faq/index.md) or reach out on Slack or via email at [compute@safe.ai](mailto:compute@safe.ai).

## **Cluster Overview**

The CAIS Compute Cluster consists of **32 GPU nodes** (Oracle Cloud bare-metal servers), each with:

| Feature                 | Description                                                                             |
| ----------------------- | --------------------------------------------------------------------------------------- |
| **GPU Nodes**           | 10 GPU nodes (Oracle Cloud bare-metal), each with 8× NVIDIA A100 80GB GPUs (total 80)  |
| **CPU Cores**           | Dual 64-core AMD CPUs per node (total 1280 CPU cores across the cluster)                |
| **Local NVMe SSD**      | 27.2 TB per node (272 TB total system storage)                                          |
| **RDMA Network**        | 1,600 Gbit/sec total, providing high-bandwidth and low-latency inter-node communication |
| **Operating System**    | Ubuntu 22.04                                                                            |

The cluster is managed using Ansible and Terraform. The cluster uses [**Slurm**](guides/running-jobs/what-is-slurm.md) for job scheduling, with [**WekaFS**](https://docs.weka.io/weka-system-overview/about) for the shared distributed parallel filesystem.
