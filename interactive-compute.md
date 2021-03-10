# Interactive Compute

## Shell Access

```
srun --pty bash
```

For more information, see the *Interactive* paragraph in the [Batch Compute](batch-compute.md#interactive) page. 

## Jupyter :id=jupyter

We provide automatic tunnels through our [ondemand](https://openondemand.org/) proxy of [Jupyter](https://jupyter.org/) instances. This means that in order to run Jupyter kernels on SDF, you do not need to setup a chain of SSH tunnels in order to show the Jupyter web instance.

To launch an instance of Jupyter, you can use the [Jupyter portal](/pun/sys/dashboard/batch_connect/sys/slac-ood-jupyter/session_contexts/new ':ignore').

?> __Note:__ As the Jupyter instances run on top of our [slurm](batch-compute.md) environment, your instances will be subject to queuing and time limits. It is recommended that if Jupyter is vital to your analysis, that [hardware be added to SDF](resources-and-allocations.md#contributing-to-sdf) to ensure priority non-preemptive access.

### 'bring-your-own-Jupyter'

We also provide the capability for you to 'bring-your-own-Jupyter' so that all your code dependencies are dictated by you, and not by us. We recommend you do this by either building a singularity image of your Jupyter environment or by building a conda environment on SDF storage.

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

## Matlab

Launch [web based access](/pun/sys/dashboard/batch_connect/sys/slac-ood-matlab/session_contexts/new)

## Ansys
