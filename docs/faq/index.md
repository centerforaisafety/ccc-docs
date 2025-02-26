# Frequently Asked Questions (FAQ)

**Q: My job is stuck in the queue.**  
A: Likely the cluster is busy or your resource request is large. Check `squeue -u <username>` or `scontrol show job <jobID>` for reasons. During conference deadlines, expect longer wait times. If unsure, ask in Slack #help-desk.

**Q: I got an "Out of memory" error.**  
A: This may be GPU OOM or system RAM OOM. Reduce batch size/model size for GPU OOM. For system memory OOM, request high-memory nodes or optimize memory usage.

**Q: How do I use multiple GPUs?**  
A: Request multiple GPUs in SLURM (`--gres=gpu:N`) and configure your code or framework (e.g., PyTorch `torch.distributed`, Lightning, or Accelerate). See [Distributed Training Example][TODO-link].

**Q: Can I run multiple jobs at once?**  
A: Yes, the scheduler allows multiple concurrent jobs. Fair-share might lower your priority if you exceed usage relative to others. Use job arrays for large sweeps.

**Q: I need software that requires sudo.**  
A: You do not have sudo access. Use user-space installs, or containerize your environment with Singularity.

For additional questions, see the [Support & Contact](support-contact.md) page or ask on Slack.