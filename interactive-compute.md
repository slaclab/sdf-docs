# Interactive Compute

## Shell Access

```
srun --pty
```


## Jupyter

We provide automatic tunnels through our [ondemand](https://openondemand.org/) proxy of [Jupyter](https://jupyter.org/) instances. This means that in order to run Jupyter kernels on SDF, do not need to setup a chain of SSH tunnels in order to show the Jupyter web instance.

We also provide the capability for you to 'bring-your-own-Jupyter' so that all your code dependencies are dictated by you, and not by us. We recommend you do this by either building a singularity image of your Jupyter environment or by building a conda environment on SDF storage.

!> __TODO:__ more information required.

To launch an instance of Jupyter, you can use the [Jupyter portal](/pun/sys/dashboard/batch_connect/sys/slac-ood-jupyter/session_contexts/new).

?> __Note:__ As the Jupyter instances run on top of our [slurm](batch-compute.md) environment, your instances will be subject to queuing and time limits. It is recommended that if Jupyter is vital to your analysis, that [hardware be added to SDF](resources-and-allocations.md#contributing-to-sdf) to ensure priority non-preemptive access.

## Matlab

Launch [web based access](/pun/sys/dashboard/batch_connect/sys/slac-ood-matlab/session_contexts/new)

## Ansys
