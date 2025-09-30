# 'bring-your-own-Jupyter'

We also provide the capability for you to 'bring-your-own-Jupyter' so that all your code dependencies are dictated by you, and not by us. We recommend you do this by either building an apptainer image of your Jupyter environment or by building a conda environment on SDF storage.

If you wish for your jupyter environment to be more widely used (e.g. for others in your group), you can submit a pull-request to our [slac-ood-jupyter repo](https://github.com/slaclab/slac-ood-jupyter) to append your specific "Commands to initiate Jupyter" onto the list of preselectable Jupyter Images. Specifically, you will want to change [form.yml.erb](https://github.com/slaclab/slac-ood-jupyter/blob/master/form.yml.erb).

## In a Conda environment

Once you have created your Conda environment on SDF (see [Software/Conda](reference.md#conda)), ensure that you have jupyter installed in your conda environment:

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


## In a container (such as Apptainer)

Once you have built or pulled an Apptainer or other OCI container image on SDF (see [Software/Apptainer](software.md#apptainer) page for more information on how to do that), ensuring that you have the `jupyter[lab]` binary in the image's `PATH`, go to the [Jupyter portal](/pun/sys/dashboard/batch_connect/sys/slac-ood-jupyter/session_contexts/new ':ignore'), select "Custom Apptainer Image" from the "Jupyter Instance" dropown menu. Then modify the text in the "Commands to initiate Jupyter":
```bash
export APPTAINER_IMAGE_PATH=<path to apptainer image>
function jupyter() {
  apptainer \
    exec \
    --nv \
    -B /sdf,/fs,/sdf/scratch,/lscratch \
    ${APPTAINER_IMAGE_PATH} \
    jupyter $@;
}
```

Replace `<path-to-the.sif>` with a path to the image you want to use for jupyter. For example, `<path-to-the.sif>` could be:
- The full path to an image you've already built on SDF: For example, if you ran `apptainer build` in your home directory, the image path may be `/sdf/home/u/username/my-special-jupyter.sif`
- A tag available publicly on a remote registry (for example, `docker://jupyter/datascience-notebook:lab-4.0.7`) would download and use [a specific version of Jupyter Lab](https://hub.docker.com/layers/jupyter/datascience-notebook/lab-4.0.7/images/sha256-9504f4f4ab7e89b49d61d7be2e9ff8c57870de2050aa4360f55b2e59193f7486?context=explore) already packaged into a container by Project Jupyter.
  - Note: If you use this method, the image will still need to be downloaded onto SDF and will (by default) take up disk space in your home directory under `~/.apptainer` to store the resulting image.

By default `apptainer` overrides your terminal prompt with `Apptainer> ` in order to emphasize that you are opening a terminal within a container.
If you prefer a less stark reminder you may instead include the following lines in `~/.bashrc` for a more familiar prompt with a subtler `(apptainer)` prefix indicating the environment is within a container.
```bash
# add a prefix if this shell is in a container
export PROMPT_COMMAND='[ -f /singularity ] && PS1="(apptainer) ${PS1}"; unset PROMPT_COMMAND'
```
This would make the terminals that you open in Jupyter Lab appear with your customary prompt, except for the additional `(apptainer) ` prefix.

Complete the rest of the form as you would for any provided Jupyter Instance and click "Launch". If you run into any issues, please see [Debugging your interactive session](#debugging).


## Debugging your interactive session :id=debugging

If you get an error while using your Jupyter instance, go to the [My Interactive sessions page](https://s3df.slac.stanford.edu/pun/sys/dashboard/batch_connect/sessions), identify the session you want to debug and click on the **Session ID** link. You can then *View* the `output.log` file to troubleshoot.


