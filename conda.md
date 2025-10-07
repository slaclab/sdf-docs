# Conda

It is not recommended to store your conda environments in your $HOME due to 1) quota limits, and 2) an inability to share conda environments across groups. We generally recommend that you install software into your facility's group space (e.g., `/sdf/group/<facility>/sw` - please see [facility storage](getting-started.md#group)). The following instructions for deploying Miniconda assume that you have write permissions in those directories. If you require write access, please consult with your facility's computing czar. The czar(s) for an S3DF facility can be found [here](https://coact.slac.stanford.edu/facilities).

## Option 1) Install Miniconda - *recommended for an entire facility*

Download the latest version of Miniconda from the [conda](https://docs.conda.io/en/latest/miniconda.html) website and follow the [Instructions](https://conda.io/projects/conda/en/latest/user-guide/install/linux.html#installing-on-linux). Change the installion `prefix` to point to an appropriate [facility directory](getting-started.md#group) replacing `<facility>` with the name of your facility as follows:

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O /tmp/Miniconda3-latest-Linux-x86_64.sh
bash /tmp/Miniconda3-latest-Linux-x86_64.sh -p /sdf/group/<facility>/sw/conda/
```

Add the newly installed conda binary to your `$PATH` environment variable:

```bash
export PATH=${PATH}:/sdf/group/<facility>/sw/conda/bin
```

Modify your local [~/.condarc](https://conda.io/projects/conda/en/latest/user-guide/configuration/use-condarc.html) file to enable the creation of new envs and installation of packages to your facility's conda install directory:

```bash
channels:
  - defaults
  - anaconda
  - conda-forge
  - pytorch
envs_dirs:
  - /sdf/group/<facility>/sw/conda/envs
pkgs_dirs:
  - /sdf/group/<facility>/sw/conda/pkgs
auto_activate_base: false
```

### Create a conda environment

Conda environments are a nice way of switching between different software versions/packages without multiple conda installs.

There is no unique way to create a conda environment, we illustrate here how to do so from a .yaml file (see the conda [documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-from-an-environment-yml-file) for more details).

In order to create an environment called `mytest` with `python=3.12` and the `numpy` and `pandas` packages installed, create `mytest-env.yaml`:
```bash
name: mytest
dependencies:
  - python=3.12
  - numpy
  - pandas
```

Then run the following command: `conda env create -f mytest-env.yaml`.

If successful, you should see `mytest` when listing your environments: `conda env list`. 

You can now activate your environment and use it: `conda activate test`. To double-check that you have the right packages, you can type `conda list` once in the environment and check that you see `numpy` and `pandas`.

## Option 2) Create and/or pull a Conda container

### Method 1 - Using Apptainer

Apptainer can be used directly on S3DF to build a specific Conda environment within a container and run it. In addition to providing a desired Conda enviroment as exampled above in `mytest-env.yaml`, an apptainer definition file specifies the image-building procedure for installing Conda and the desired environment packages. To start, create `mytest-app.def`:
```apptainer
Bootstrap: docker
From: continuumio/miniconda3:latest

%files
    mytest-env.yaml /mytest-env.yaml

%post
    /opt/conda/bin/conda env create -f /mytest-env.yaml

%environment
    source /opt/conda/etc/profile.d/conda.sh
    conda activate mytest

%runscript
    exec "$@"
```

To build the image (.sif file) run the command:

`apptainer build --fakeroot mytest-env-image.sif mytest-env.def` 

This should create a container image `mytest-env-image.sif` which contains the desired conda environment settings.

To use this apptainer interactively, simply run:

`apptainer shell mytest-env-image.sif`

which opens a terminal prompt within the image with the conda environment activated. Then, from within the Apptainer shell, running `python` opens a python terminal in the installed conda environment.

Alternatively, the apptainer can be used as an executable to run a desired python script (e.g. `my_script.py`) by using the command:

`apptainer run mytest-env-image.sif python my_script.py`

where the arguments following the .sif image are to be run as code within the container.

Note: that container images are immutable and must be rebuilt any time changes are needed in the conda environment.

### Method 2 - Using Docker
