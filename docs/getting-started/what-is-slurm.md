# Slurm

## **What is Slurm?**

Slurm (Simple Linux Utility for Resource Management) is an open-source workload manager and job scheduler for high-performance computing (HPC) clusters. It automates job queuing, scheduling, and resource allocation (e.g., CPUs, memory, GPUs) so multiple users can efficiently share a cluster.

### **Why Use Slurm?**
| Feature                 | Description                                                     | 
| ----------------------- | --------------------------------------------------------------- |
| **Job Scheduling**      | Automatically queues and runs jobs when resources become available |
| **Resource Management** | Allocates CPUs, memory, and GPUs to each job without conflicts |
| **Automation**          | Runs jobs even if you’re logged off, collecting outputs for later review |
| **Fairness & Scalability** | Enforces usage policies (priorities, fair-share) and scales to thousands of nodes |

### **Key Features**
| Feature                           | Description                                                                                          |
| --------------------------------- | ---------------------------------------------------------------------------------------------------- |
| **Job Queueing & Prioritization** | Places submitted jobs in a queue and assigns resources based on configurable policies                |
| **GPU & Parallel Workloads**      | Easily requests and manages GPUs or multiple nodes for distributed computing                         |
| **Monitoring & Reporting**        | Tracks job status, usage statistics, and logs outputs                                                |

### **How It Works (Simplified)**
| Step                                  | Description                                                              |
| ------------------------------------- | ------------------------------------------------------------------------ |
| **1. Submit a Job**                   | Provide required resources (e.g. `sbatch my_job.sh`).                     |
| **2. Queue & Scheduling**             | Slurm queues your job until the requested resources are free.             |
| **3. Resource Allocation & Execution** | Allocates a compute node (or nodes) to your job and launches it.        |
| **4. Completion**                     | Frees resources for new jobs; job results are saved for review.           |

### **External Resources**
| Resource                           | Link                                                                                                 |
| ---------------------------------- | ---------------------------------------------------------------------------------------------------- |
| **Slurm Official Documentation**   | [https://slurm.schedmd.com/documentation.html](https://slurm.schedmd.com/documentation.html)         |
| **Slurm Quick Start Guide**        | [https://slurm.schedmd.com/quickstart.html](https://slurm.schedmd.com/quickstart.html)               |
| **Beginner-Friendly Tutorial**     | [Ronin: Slurm Guide for Beginners](https://blog.ronin.cloud/slurm-intro/)                            |