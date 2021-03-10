# Software



!> Please note that we are effectively treating the design and implementation of SDF as a green field deployment. As such certain technologies and tools may not be available. Please [contact us](contact-us.md) if you wish for anything to be added or removed.

## I Need Software X...

### Environment Modules

#### SDF Provided Modules

#### Adding Your Own Modules


## Where Do I Install Software?

### Conda

It is not recommended to store your conda environments in your $HOME due to 1) quota limits, and 2) an inability to share conda environments across groups. We generally recommend that you install software into your $GROUP space (eg `/sdf/group/<group_name>/sw` - please see [Group storage](getting-started.md#group)).

#### Install Miniconda

Download the latest version of Miniconda from the [conda](https://docs.conda.io/en/latest/miniconda.html) website and follow the [Instructions](https://conda.io/projects/conda/en/latest/user-guide/install/linux.html#installing-on-linux). Change the `prefix` to 

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O /tmp/Miniconda3-latest-Linux-x86_64.sh
bash /tmp/Miniconda3-latest-Linux-x86_64.sh -p /sdf/group/<group_name>/sw/conda/
```

Replacing `<group_name>` appropriately.

We can also modify our [~/.condarc](https://conda.io/projects/conda/en/latest/user-guide/configuration/use-condarc.html) file as follows;

```bash
channels:
  - defaults
  - anaconda
  - conda-forge
  - pytorch
envs_dirs:
  - /sdf/group/<group_name/sw/conda/envs
pkgs_dirs:
  - /sdf/group/<group_name/sw/conda/pkgs
auto_activate_base: false
```

#### Create a conda environment

Conda environments are a nice way of switching between different software versions/packages without multiple conda installs.

There is no unique way to create a conda environment, we illustrate here how to do so from a .yaml file (see the conda [documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-from-an-environment-yml-file) for more details).

In order to create an environment called `mytest` with `python=3.6` and `numpy` and `pandas` in it, create `mytest-environment.yaml`:
```bash
name: mytest
dependencies:
  - python=3.6
  - numpy
  - pandas
```

Then run the following command: `conda env create -f mytest-environment.yaml`.

If successful, you should see `mytest` when listing your environments: `conda env list`. 

You can now activate your environment and use it: `conda activate test`. To double-check that you have the right packages, you can type `conda list` once in the environment and check that you see `numpy` and `pandas`.


### Singularity

For a detailed explanation of how to use Singularity on SDF, you can go through Yee-Ting Li's presentation [here](https://confluence.slac.stanford.edu/display/AI/AI+Seminar#AISeminar-Containers!Containers!Containers!) where you can find both the slides and the zoom recording.

#### Prerequisite

As pulling and building a new image can use quite a lot of disk space, we recommend that you set the appropriate cache paths for singularity to not use your $HOME directory. Therefore, before pulling or building an image, define the following environment variables:

```bash
export DIR=/scratch/${USER}/.singularity
mkdir $DIR -p
export SINGULARITY_LOCALCACHEDIR=$DIR
export SINGULARITY_CACHEDIR=$DIR
export SINGULARITY_TMPDIR=$DIR
```

#### Pulling images

To pull an image from DockerHub, do:
```bash
singularity pull docker://<user or organization>/<repository>:<tag>
```

## Compiling Software

### GCC

### Intel Compilers


### OpenMPI

### OpenMP


## Pre-packaged Sofware

### Jupyter

### PyTorch

### Tensorflow

### MatLab

### Ansys


## Revision Control and Git


