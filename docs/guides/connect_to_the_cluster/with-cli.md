# How to connect to the cluster

## How to connect with CLI
```bash
ssh -i ~/.ssh/your_private_key <username>@compute.safe.ai
```
- You can create an SSH config alias if you wish.  
- You'll land on the login node.   
- When done, type `exit` to terminate the session.  
- Interactive sessions are for quick debugging; use batch jobs for long runs.

???+ Warning
    Please do not run heavy computations on the login node. This includes installing things (request a CPU node to do so).