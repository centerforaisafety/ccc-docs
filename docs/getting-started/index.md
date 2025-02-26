# Getting Started

## Access
- Have your PI (Principal Investigator) reach out to a CAIS Compute Cluster admin.
- Once approved, you **will** receive a username.

## Logging in
Access to the CAIS Compute Cluster is provided via Secure Shell ([SSH](/ccc-docs/guides/connect/what-is-ssh/)) login. Most Unix-like operating systems provide an SSH client by default that can be accessed by typing the ssh command in a terminal window.

To login, open a terminal and type the following command, where <username> should be replaced with the username you were provided with:

```sh
$ ssh -i ~/.ssh/id_ed25519 <username>@compute.safe.ai
$ <username>@cais-login-0:~$
```

Upon logging in, you will be connected to a login node (e.g., `cais-login-0`).

!!! warning "Login nodes are not for computing"
    Login nodes are shared among many users and must not be used for computationally intensive tasks. 
    Instead, submit those tasks to the scheduler, which will dispatch them to the compute nodes.

## Getting compute
Get an interactive session on a node with a single GPU and two CPU cores (the default ratio is 2 CPUs per GPU):
```sh
$ <username>@cais-login-0:~$ srun --gpus=1 --pty /bin/bash
$ <username>@compute-permanent-node-535:~$
```
Run a command
```sh
$ <username>@compute-permanent-node-535:~$ nvidia-smi
Tue Feb 25 22:08:12 2025       
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
+-----------------------------------------------------------------------------------------
```
!!! tip "How-To Guides"
    After gaining access to the cluster, you can familiarize yourself with it using our How-To Guides.
    They include information on connecting to the cluster, running jobs, general cluster usage, and more.

