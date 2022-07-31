# Interactive Compute

## Terminal

Once you land on the login nodes, either via a terminal or via a NoMachine desktop, you will need to ssh to one of the interactive pools to access the data, build/debug your code, run simple analyses, or submit jobs to the [batch system](batch-compute.md). If your organization has acquired dedicated resources for the interactive pools, use them; otherwise, connect to the S3DF shared interactive pool. Currently, the available pools are:

|Pool name | Organization(s) | Resources |
| --- | --- | --- |
|s3dfana | All (shared pool) | 2 servers, 256 cores |
|rubin-devl | Rubin | 2 servers, 256 cores |
|cdms | CDMS, SuperCDMS | 2 servers, 256 cores |

### Interactive session using Slurm

Under some circumstances, for example if you need more, or different, resources than available in the interactive pools, you may want to run an interactive session using resources from the batch system. This can be achieved through the Slurm command srun:

```
srun --partition <partitionname> -n 1 --time=01:00:00 --pty /bin/bash
```

This will execute `/bin/bash` on a (scheduled) server in the Slurm partition `<partitionname>`, allocating a single CPU for one hour, and launching a pseudo terminal (pty) where bash will run. See [batch banking](batch-compute.md#banking) to understand how your organization is charged (computing time, not money) when you use the batch system.

Note that when you 'exit' the interactive session, it will relinquish the resources for someone else to use. This also means that if your terminal is disconnected (you turn your laptop off, loose network etc), then the Job will also terminate (similar to ssh).

To support X11, add the "--x11" option:

```
srun --x11 --partition shared -n 1 --time=01:00:00 --pty /bin/bash
```

## Browser

Users can also access S3DF through Open OnDemand via any (modern) browser at [https://s3df.slac.stanford.edu/ondemand](https://s3df.slac.stanford.edu/ondemand). This solution is recommended for users who want to run Jupyter notebooks, or don't want to learn SLURM, or don't want to download a terminal or the NoMachine remote desktop on their system. After login, you can select which Jupyter image to run and which hardware resources to use (partition name and number of hours/cpu-cores/memory/gpu-cores). The partition can be the name of an interactive pool or the name of a SLURM partition. You can choose an interactive pool as partition if you want a long-running session requiring sporadic resources; otherwise slect a SLURM partition. Note that no GPUs are currently available on the interactive pools.

### Shell

### Jupyter :id=jupyter

We provide automatic tunnels through our [ondemand](https://openondemand.org/) proxy of [Jupyter](https://jupyter.org/) instances. This means that in order to run Jupyter kernels on SDF, you do not need to setup a chain of SSH tunnels in order to show the Jupyter web instance.

To launch an instance of Jupyter, you can use the [Jupyter portal](/pun/sys/dashboard/batch_connect/sys/slac-ood-jupyter/session_contexts/new ':ignore').

?> __Note:__ As the Jupyter instances run on top of our [slurm](batch-compute.md) environment, your instances will be subject to queuing and time limits. It is recommended that if Jupyter is vital to your analysis, that [hardware be added to SDF](resources-and-allocations.md#contributing-to-sdf) to ensure priority non-preemptive access.

### 'bring-your-own-Jupyter'

We also provide the capability for you to 'bring-your-own-Jupyter' so that all your code dependencies are dictated by you, and not by us. We recommend you do this by either building a singularity image of your Jupyter environment or by building a conda environment on SDF storage.

If you wish for your jupyter environment to be more widely used (e.g. for others in your group), you can submit a pull-request to our [slac-ood-jupyter repo](https://github.com/slaclab/slac-ood-jupyter) to append your specific "Commands to initiate Jupyter" onto the list of preselectable Jupyter Images. Specifically, you will want to change [form.yml.erb](https://github.com/slaclab/slac-ood-jupyter/blob/master/form.yml.erb).

#### in a Conda environment

Once you have created your Conda environment on SDF (see [Software/Conda](software.md#conda)), ensure that you have jupyter installed in your conda environment:

```
conda install -c conda-forge jupyterlab
```

Then go to [Jupyter portal](/pun/sys/dashboard/batch_connect/sys/slac-ood-jupyter/session_contexts/new ':ignore'), and select "Custom Conda Environment..." from the "Jupyter Instance" dropdown. You will need to customize the text that appears under "Commands to initiate Jupyter" to point to your custom conda environment:

```bash
export CONDA_PREFIX=<path-to-miniconda3>
export PATH=${CONDA_PREFIX}/bin/:$PATH
source ${CONDA_PREFIX}/etc/profile.d/conda.sh
conda env list
conda activate <your-environment-name>
```

Replace `<path-to-miniconda3>` and `<your-environment-name>` appropriately.

Fill the rest of the form as you would for any provided Jupyter Instance and click "Launch". If you run into any issues, please see [Debugging your interactive session](#debugging).


#### in a Singularity container

Once you have built or pulled a Singularity image on SDF (see [Software/Singularity](software.md#singularity) page for more information on how to do that), ensuring that you have the `jupyter[lab]` binary in the image's `PATH`, go to the [Jupyter portal](/pun/sys/dashboard/batch_connect/sys/slac-ood-jupyter/session_contexts/new ':ignore'), select "Custom Singularity Image" from the "Jupyter Instance" dropown menu. Then modify the text in the "Commands to initiate Jupyter":
```bash
export SINGULARITY_IMAGE_PATH=<path-to-the.sif>
function jupyter() { singularity exec --nv -B /sdf,/gpfs,/scratch,/lscratch ${SINGULARITY_IMAGE_PATH} jupyter $@; }
```

Replace `<path-to-the.sif>` with the full path to your local singularity image file.

Fill the rest of the form as you would for any provided Jupyter Instance and click "Launch". If you run into any issues, please see [Debugging your interactive session](#debugging).


### Debugging your interactive session :id=debugging

If you get an error while using your Jupyter instance, go to the [My Interactive sessions page](https://sdf.slac.stanford.edu/pun/sys/dashboard/batch_connect/sessions), identify the session you want to debu and click on the **Session ID** link. You can then *View* the `output.log` file to troubleshoot.

#### Matlab

Launch [web based access](/pun/sys/dashboard/batch_connect/sys/slac-ood-matlab/session_contexts/new)
