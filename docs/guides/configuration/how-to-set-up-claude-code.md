# How to Set Up Claude Code on the OCI-HPC Cluster

## What is Claude Code?

Claude Code is Anthropic's command-line coding agent. It runs in your terminal and can read files, write code, and execute commands on your behalf. On this cluster, we provide a shared configuration that teaches Claude the rules of our environment — Slurm, shared filesystems, GPU etiquette, and common pitfalls — so it behaves as a responsible cluster citizen from the first session without repeated, explicit instructions by the user.

## Prerequisites

- An active Claude Pro or Max subscription, or an Anthropic API key
- SSH access to the cluster

## Step 1: Install Claude Code

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

Verify it installed:

```bash
claude --version
```

## Step 2: Go to Your User Directory

Always start from your workspace on the shared filesystem:

```bash
cd /data/$USER
```

This is where all your projects, conda environments, datasets, and outputs should live. Never work out of `$HOME` for anything large — home directory quotas are small.

You may want to add this to your `~/.bashrc` so you land here on every login:

```bash
echo 'cd /data/$USER' >> ~/.bashrc
```

## Step 3: Authenticate

Run `claude` once to trigger the login flow. It will open a browser URL — if you're connected via SSH, copy the URL and open it on your local machine to complete authentication. 
Copy the code back to terminal and press "Enter". 

If you're using an API key instead of a subscription:

```bash
export ANTHROPIC_API_KEY="sk-ant-..."
```

Add that export to your `~/.bashrc` to persist it across sessions.

## Step 4: Set Up the Cluster Protocol

We maintain a shared file at `/data/claude/cluster-citizen.md` that teaches Claude the rules of this cluster — Slurm partitions, filesystem boundaries, GPU etiquette, cgroup limits, and common pitfalls.

To load it, use the `--append-system-prompt-file` flag when starting Claude:

```bash
claude --append-system-prompt-file /data/claude/cluster-citizen.md
```

This appends the cluster rules to Claude's default instructions. Your personal `~/.claude/CLAUDE.md` and any project-level settings still work normally — nothing is overwritten.

### Make it the default

To avoid typing the flag every time, add an alias to your `~/.bashrc`:

```bash
echo 'alias claude="claude --append-system-prompt-file /data/claude/cluster-citizen.md"' >> ~/.bashrc
source ~/.bashrc
```

Now just typing `claude` loads the cluster protocol automatically.

### Verify it's working

Start a session and ask:

```
> What partitions are available on this cluster?
```

Claude should respond with `cais`, `cais_cpu`, `tamper_resistance`, and `tamper_resistance_cpu` without you needing to tell it.

## Step 5 (Optional): Add Your Own CLAUDE.md

The cluster protocol covers shared rules. For your own project-specific context, create a `CLAUDE.md` in your project directory:

```bash
cd /data/$USER/my-project
cat > CLAUDE.md << 'EOF'
# My Project

- Python 3.11, PyTorch 2.x
- Conda env: myenv
- Tests: pytest tests/
- Data lives in /data/$USER/datasets/imagenet/
EOF
```

Claude loads this automatically when you run `claude` from that directory. It stacks with the cluster protocol — both apply.

## Usage Tips

### Always use Slurm for heavy work

Claude knows this rule, but reinforce it by telling Claude what you're doing:

```
> I need to train a model on 2 GPUs for ~6 hours. Write me an sbatch script.
```

Claude will use the correct partition names and resource flags for this cluster.

### Use conda, not pip --user

All Python environments should be conda envs stored under `/data/$USER/`. If you don't have miniconda yet:

```bash
curl https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -o /tmp/miniconda.sh
bash /tmp/miniconda.sh -b -p /data/$USER/miniconda3
/data/$USER/miniconda3/bin/conda init bash
# Close and reopen your shell, then:
conda create -n myenv python=3.11 -y
conda activate myenv
```

### Set HuggingFace cache to /data

If you download models from HuggingFace, make sure the cache doesn't fill your home directory:

```bash
echo 'export HF_HOME=/data/$USER/.cache/huggingface' >> ~/.bashrc
source ~/.bashrc
```

### Reporting mistakes

If Claude does something wrong that other users should be protected from — like trying to run training on the login node, or installing packages to the wrong location — report it to **[maintainer name / Slack channel]**. We maintain a shared lessons file that gets updated so every Claude session on the cluster learns from past mistakes.

## Quick Reference

| What | Command |
|---|---|
| Start Claude | `claude` |
| Check Slurm queue | `squeue -u $USER` |
| Interactive GPU session | `salloc --partition=cais --gres=gpu:1 --time=01:00:00` |
| Submit batch job | `sbatch job.slurm` |
| Cancel a job | `scancel <jobid>` |
| Check GPU availability | `sinfo -p cais --format="%N %G %t"` |
| Activate conda env | `conda activate myenv` |

## Troubleshooting

### "command not found: claude"
The install script may not have added Claude to your PATH. Try opening a new shell, or run `source ~/.bashrc`. If it still fails, check that `~/.claude/bin` (or wherever the installer placed it) is in your PATH.

### Claude doesn't know about the cluster
The alias isn't set. Run `alias claude` to check. If it doesn't show the `--append-system-prompt-file` flag, re-run the Step 3 command.

### Authentication fails over SSH
Copy the URL Claude prints and open it in a browser on your local machine. Complete the login there. The CLI will detect the auth automatically.

### Claude tries to run training on the login node
Tell it explicitly: "This must go through Slurm." If the cluster protocol is loaded, Claude should already know this — if it doesn't, check that your alias is set correctly.

### Home directory is full
Likely caused by pip/conda installing to `$HOME`. Move your conda installation to `/data/$USER/miniconda3` and set `HF_HOME` as described above.

Contact the administrator if none of the solutions are satisfactory.