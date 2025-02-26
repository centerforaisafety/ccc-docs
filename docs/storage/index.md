# Storage

The CAIS Compute Cluster is equipped with a distributed parallel filesystem that is deployed across the compute nodes.

The CCC has a single filesystem mounted to `/data`. In this filesystem we store all of our data such as user home directories, shared group directories,  models, and datasets.

Each user get 500GB of storage in their home directories.

Each group gets a shared storage directory with 1TB of available space.

We use Weka as our filesystem tech. Weka uses the local ssds available on compute nodes. Due to this, you are unable to use the local ssds of a compute node directly.

## Quotas and limits

Each users home directory has a quota of 500GB.

Each groups shared directory has a quota of 1TB.

