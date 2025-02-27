# Frequently Asked Questions (FAQ)

**Q: My job is stuck in the queue.**  
A: Likely the cluster is busy or your resource request is large. Check `squeue -u <username>` or `scontrol show job <jobID>` for reasons. During conference deadlines, expect longer wait times. If unsure, ask in Slack #help-desk.

**Q: How do I request multiple GPUs?**  
A: Request multiple GPUs in Slurm (`--gpus-per-node=:N`).

**Q: Can I run multiple jobs at once?**  
A: Yes, the scheduler allows multiple concurrent jobs. Fair-share might lower your priority if you exceed usage relative to others.

**Q: I need software that requires sudo.**  
A: You do not have sudo access. If you are unable to install the software you need yourself through `pip` or `conda` please reach out to an admin.

For additional questions, ask a question on Slack in the help desk channel.