# Batch Compute

## Slurm

Slurm is a batch scheduler that enables users to submit compute jobs
of varying scope to our compute clusters. It will queue up jobs such
that the compute resources available in S3DF are fairly and
efficiently shared and distributed for all users. This page describes
S3DF specific Slurm information. If you haven't used Slurm before, you
can find general information on using this workflow manager in our
[Slurm reference FAQ](reference.md#SlurmFAQ).

## Clusters & Repos

A cluster is a homogeneous set of computing nodes with the same
hardware specifications and the same access to the storage. A facility
is a program/project which can buy resources (e.g., LCLS, Rubin,
SUNCAT, SuperCDMS, etc). A repo is a set of resources associated with
a group of people within a facility (e.g., an LCLS experiment or a
cryo-EM experiment). Not all repos will have access to all
clusters. Some repos will have dedicated resources within a cluster,
while some will use shared resources.

### Partitions & Accounts

For submitting jobs, you need to specify a two-ple: the cluster
(--partition in Slurm terminology) and the repo (--account in
Slurm). These two parameters indicate, respectively, which hardware to
use and repo to charge for that particular job. Use coact to determine
how many computing hours your repo has on a specific cluster.

![clusters](assets/s3df-slurm-clusters.png)

Each repo can have one of three stances in relation to a specific
cluster:

1. Dedicated resources: for repos with real time requirements or with
  uniform usage over time (for that cluster).

2. Shared resources with priority: for repos within their quota (for
  that cluster).

3. Shared resources without priority: for repos above their quota (for
  that cluster). Jobs in this category may be preempted by higher
  priority jobs.

The mapping of repos to dedicated resource is dynamic. This is
required, for example, to assign different nodes to a repo so that a
rolling upgrade does not cause an outage for stance 1, or to change
the amount of resources dedicated to real-time and fast-feedback
activities within a cluster to match the actual requirements of a
running experiment.

![repostance](assets/s3df-slurm-repostance.png)


See the table below to determine the specifications for each
cluster/partition.

| Partition name | CPU model | Cores per node | Memory per node | GPU model | GPUs per node | Local scratch | Number of nodes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| roma | Rome 7702 | 128 | 512 GB | - | - | 960 GB | 26 |
| ampere | Rome 7542 | 64 | 1024 GB | Tesla A100 | 4 | 12 TB | 6 |
| turing | Intel 12 Gold | 48 | 192 GB | 2080 Ti | 10 | 960 GB | 2 |



### Banking

The coact system will keep track of the hours spent by each repo on
each clusters. Once a repo reaches its computing quota on a cluster,
further submissions to that cluster will have lower priority. Note:
depending on the initial experience, we may also limit the resources
available to over-quota repos (i.e., by enforcing a cap on the amount
of cores, or memory, a job may take), and allow higher priority jobs
to preempt lower priority ones. Allocations will reset on a calendar
year boundary, i.e., on December 31st

