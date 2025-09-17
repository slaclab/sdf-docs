# SLURM Constraint Usage for S3DF

## SLURM Constraints
Batch nodes at S3DF have static features assigned to them in the slurm.conf. Users can specify which of those features are required by their jobs using the constraint option via `srun` or `sbatch`. Only nodes with active features matching the job constraints will be used by the SLURM controller to satisfy the job request.
Multiple constraints may be specified during job submission. Please refer to the official documentation for more information. https://slurm.schedmd.com/sbatch.html

## Active Features

As mentioned, the batch nodes have active features, and servers that belong to the same partition have homogeneous software and hardware. However, for the `partition=milano`, S3DF supports some subtle hardware differences. For example, some nodes have more memory than others, which can be identified via active features.

Example
```
scontrol show node sdfmilan[001-274] | awk '{for (i=1;i<=NF;i++) if ($i ~ /^NodeName=/ || $i ~ /^ActiveFeatures=/) print $i}'
...
NodeName=sdfmilan267
ActiveFeatures=CPU_GEN:MLN,CPU_SKU:7713,CPU_FRQ:2.00GHz,CPU_MNF:AMD,OS_ID:RHEL,OS_VER:8.6,CrowdStrike_off,MEM_SZE:480GB
NodeName=sdfmilan268
ActiveFeatures=CPU_GEN:MLN,CPU_SKU:7713,CPU_FRQ:2.00GHz,CPU_MNF:AMD,OS_ID:RHEL,OS_VER:8.6,CrowdStrike_off,MEM_SZE:480GB
NodeName=sdfmilan269
ActiveFeatures=CPU_GEN:MLN,CPU_SKU:7713,CPU_FRQ:2.00GHz,CPU_MNF:AMD,OS_ID:RHEL,OS_VER:8.6,CrowdStrike_on,MEM_SZE:1920GB
NodeName=sdfmilan270
ActiveFeatures=CPU_GEN:MLN,CPU_SKU:7713,CPU_FRQ:2.00GHz,CPU_MNF:AMD,OS_ID:RHEL,OS_VER:8.6,CrowdStrike_on,MEM_SZE:1920GB
NodeName=sdfmilan271
...
```
## High-Memory Node Usage and Policies

High-memory Milano nodes allow preemptable jobs by default, even if the user does not explicitly specify the constraint identifying those nodes during job submission. This policy maximizes CPU usage and prevents the creation of small silos in the S3DF cluster.
However, if users want to run preemptable jobs specifically on high-memory nodes, they must submit the jobs using the corresponding active features.
KIPAC users are allowed to run `qos=normal` jobs on these nodes. In such cases, the scheduler decides which `qos=preemptable` jobs running on the high-memory nodes must be canceled to release resources for the KIPAC `qos=normal` jobs

## Using Active Features

Running jobs on high-memory nodes using active features is straightforward:
```
sbatch --constraint="MEM_SZE:1920GB"
```
or include the same option in an `srun` script.

Note: If users outside the KIPAC facility attempt to submit `qos=normal` jobs to high-memory nodes, the submission will fail.
