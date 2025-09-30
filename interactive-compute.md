# Interactive Compute

## Using A Terminal

### Interactive Pools :id=interactive-pools 

In order to access compute and storage resources in S3DF, you will need to log onto our interactive nodes. After, login to our bastion hosts either via a [ssh terminal session or via NoMachine](access.md), you will then need to ssh to one of the interactive pools to access the data, build/debug your code, run simple analyses, or submit jobs to the [batch system](batch-compute.md). If your organization has acquired dedicated resources for the interactive pools, use them; otherwise, you can connect to the S3DF shared interactive pool.

?> Note: After log in into our bastion hosts with `ssh s3dflogin-mfa.slac.stanford.edu`, you will need to then need to log into our interactive nodes to access batch compute and data. You can do this via `ssh <pool name>` within your ssh session (same terminal) to get into the bastion hosts.

The currently available pools are shown in the table below (The facility can be any organization, program, project, or group that interfaces with S3DF to acquire resources).

|Pool name | Facility | Resources |
| --- | --- | --- |
|iana | For all S3DF users | 4 servers, 40 HT cores and 384 GB per server |
|rubin-devl | Rubin | 4 servers, 128 cores and 512 GB per server |
|psana | LCLS | 4 servers, 40 HT cores and 384 GB per server |
|fermi-devl | Fermi | 1 server, 64 HT cores and 512 GB per server |
|faders | FADERS | 1 server, 128 HT cores and 512 GB per server |
|ldmx | LDMX | 1 server, 128 HT cores and 512 GB per server |
|ad | AD | 3 servers, 128 HT cores and 512 GB per server |
|epptheory | EPPTheory | 2 servers, 128 HT cores and 512 GB per server |
|cdms | SuperCDMS | (points to iana) |
|suncat | SUNCAT | (points to iana) |
|neutrino | Neutrino |  (points to iana) |
|mli | MLI (ML Initiative) |  (points to iana) |

### Interactive Compute Session Using Slurm

Under some circumstances, for example if you need more, or different, resources than available in the interactive pools, you may want to run an interactive session using resources from the batch system. This can be achieved through the Slurm command srun:

```
srun --partition <partitionname> --account <accountname> -n 1 --time=01:00:00 --pty /bin/bash
```

This will execute `/bin/bash` on a (scheduled) server in the Slurm partition `<partitionname>` (see [partition names](batch-compute.md#partitions-amp-accounts)), allocating a single CPU for one hour, charging the time to account `<accountname>` (you'll have to get this information from whoever gave you access to S3DF), and launching a pseudo terminal (pty) where `/bin/bash` will run (hence giving you an interactive terminal). See [batch banking](batch-compute.md#banking) to understand how your organization is charged (computing time, not money) when you use the batch system.

Note that when you 'exit' the interactive session, it will relinquish the resources for someone else to use. This also means that if your terminal is disconnected (you turn your laptop off, loose network etc), then the job will also terminate (similar to ssh).

To support tunnelling X11 back to your computer, add the "--x11" option:

```
srun --x11 --partition <partitionname> --account <accountname> -n 1 --time=01:00:00 --pty /usr/bin/xterm
```

## Using A Browser and OnDemand

Users can also access S3DF through [Open OnDemand](https://s3df.slac.stanford.edu/ondemand) via any (modern) browser. This solution is recommended for users who want to run Jupyter notebooks, or don't want to learn SLURM, or don't want to download a terminal or the NoMachine remote desktop on their system. After login, you can select which Jupyter image to run and which hardware resources to use (partition name and number of hours/cpu-cores/memory/gpu-cores). The partition can be the name of an interactive pool or the name of a SLURM partition. You can choose an interactive pool as partition if you want a long-running session requiring sporadic resources; otherwise slect a SLURM partition. Note that no GPUs are currently available on the interactive pools.

### Web Shell

After login onto [OnDemand]((https://s3df.slac.stanford.edu/ondemand), select the Clusters tab and then select the
desired [interactive pool](#interactive-pools) from the pull down menu. This will allow you to
obtain a shell on the interactive pools without using a terminal.

You can also obtain direct access to the [Interactive Analysis Web Shell](https://s3df.slac.stanford.edu/pun/sys/shell/ssh/iana.sdf.slac.stanford.edu) without needing to go through a separate bastion.


### Jupyter

We provide automatic tunnels through our [ondemand](https://openondemand.org/) proxy of [Jupyter](https://jupyter.org/) instances. This means that in order to run Jupyter kernels on S3DF, you do not need to setup a chain of SSH tunnels in order to show the Jupyter web instance.

You can [launch a new juptyer session via the provided web form](https://s3df.slac.stanford.edu/pun/sys/dashboard/batch_connect/sys/slac-ood-jupyter/session_contexts/new). You may choose to run your jupyter instance on either Batch nodes or the Interactive nodes via the **Run on cluster type** dropdown. Note that with the former, you will need to select the appropriate cpu and memory resources in advance to run your notebook. Hoewver, for the latter, you will most likely be contending your jupyter resources against others who are also logged on to the interactive node.

Users are welcome to submit a github pull-request to have their Jupyter environments added to the [SLAC Open Ondemand Jupyter App](https://github.com/slaclab/slac-ood-jupyter). Please see [guide for devloping your own Jupyter environments](jupyter.md) for further information.
