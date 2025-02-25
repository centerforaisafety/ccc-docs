# Usage Policies and Best Practices

## Access and Usage
- The cluster is for **approved AI safety projects** only.
- Two access tiers:
  1. **Project-Based Access**: Full node/GPU usage within fair-share.
  2. **Limited Access**: Restricted to certain partitions/GPUs.
- Jobs exceeding 48-hour runtime or requesting huge resources may be deprioritized.

## Fair Scheduling
- SLURM’s fair-share policy ensures no single user monopolizes the cluster.
- Expect longer queues near conference deadlines.
- Use job arrays instead of flooding the scheduler with hundreds of jobs.

## Data and Security
- Do not bypass security. Home directories are private by default.
- No sharing of credentials or accounts.
- All usage is subject to monitoring.

## Acknowledging the Cluster
- If publishing work done on CAIS, include:  
  > “This research was supported by the Center for AI Safety Compute Cluster...”
- CAIS may list your project or paper on its website to show cluster impact.

## Best Practices
- **No heavy compute on login node** — always use SLURM.
- Clean up old files and logs to save space.
- Monitor your resource usage (GPU, CPU, memory) to avoid idle or wasted allocations.
- Be considerate and coordinate during peak times.

Serious or repeated violations may result in account suspension.