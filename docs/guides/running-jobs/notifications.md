# Configuration

## How to configure job notifications

We have configured SLURM for sending email and Slack notifications for various job stages (begin, fail, requeue, complete, etc) from the `do-not-reply@safe.ai` email address (check spam). It is also capable of interfacing with other notification platforms, so if you would like us to configure it for another platform, let us know and we will look into it. We are using the [goslmailer](https://github.com/CLIP-HPC/goslmailer) for the notifications.

You can add notifications to your job by adding the following lines to your SBATCH file:
```sh
#SBATCH --mail-user=mailto:{email},slack:{slack-member-id}
#SBATCH --mail-type=ALL
```
Feel free to replace `{email}` with one of your choice and `{slack-member-id}` with your personal one for the CAIS Compute Cluster workspace ([how to find your member id](https://www.workast.com/help/article/how-to-find-a-slack-user-id/)). If you would only like to use Slack or email for notifications and not the other, you can do this by only including that service in your sbatch.

Example:
```sh
#SBATCH --mail-user=mailto:{email}
#SBATCH --mail-type=ALL
```
You can also configure the messages with all the [mail-type options](https://slurm.schedmd.com/sbatch.html#OPT_mail-type) found in SLURM by default.