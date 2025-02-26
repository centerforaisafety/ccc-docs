# How to connect to the cluster

## **With the command line**
```bash
ssh -i ~/.ssh/your_private_key <username>@compute.safe.ai
```

- You'll land on the login node.   
- When done, type `exit` to terminate the session.

???+ Warning
    Please do not run heavy computations on the login node. This includes installing things (request a CPU node to do so).