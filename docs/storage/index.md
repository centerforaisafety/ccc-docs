# Storage

The CAIS Compute Cluster is equipped with a distributed parallel filesystem ([Weka](https://www.weka.io/)) deployed across all compute nodes. In the CCC, a single filesystem is mounted at `/data`. This filesystem houses:

- User home directories
- Shared group directories
- Models
- Datasets

Because Weka uses the local SSDs from compute nodes as part of the distributed filesystem, you **cannot** use a node’s local SSDs directly in a job or for storing data manually.

## **User Home Directories**

- Location: `/data/<username>`
- Quota: 500 GB per user

Your home directory is the primary space for storing personal scripts, data, and other files. If you approach your quota, you may need to delete or relocate files to free up space.

## **Shared Group Directories**

- Location: `/data/groups/<groupname>`
- Quota: 1 TB per group

Groups and labs each have a shared directory that can be used by all members of the group. These directories facilitate collaborative work, such as sharing datasets, code, and results within the group.

## **Quotas and Limits**

All quotas are enforced automatically. If you exceed your quota, you may be unable to write new data until you remove or relocate files.

- **User Home Quota:** 500 GB
- **Group Shared Quota:** 1 TB

Need more storage? [Request a quota increase](request-additional-storage.md).