# Software



!> Please note that we are effectively treating the design and implementation of SDF as a green field deployment. As such certain technologies and tools may not be available. Please [contact us](contact-us.md) if you wish for anything to be added or removed.

## I Need Software X...

### Environment Modules

#### SDF Provided Modules

#### Adding Your Own Modules


## Where Do I Install Software?

### Conda

It is not recommended to store your conda environments in your $HOME due to quota limits that might be quickly met. Instead you can use $SCRATCH. We suggest to do the following:

#### Install Miniconda3

Add the following lines to your `~/.bashrc`
```bash
export DIR=/scratch/${USER}/.conda
mkdir $DIR -p
```

Download the latest version of Miniconda from the [conda](https://docs.conda.io/en/latest/miniconda.html) website and follow the [Instructions](https://conda.io/projects/conda/en/latest/user-guide/install/linux.html#installing-on-linux); the following should work:
```bash
cd $HOME
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh 
bash Miniconda3-latest-Linux-x86_64.sh
```

Edit your `~/.condarc` as follows:
```bash
channels:
  - defaults
  - anaconda
  - conda-forge
  - pytorch
envs_dirs:
  - /scratch/${USER}/.conda/envs
pkgs_dirs:
  - /scratch/${USER}/.conda/pkgs
auto_activate_base: false
```

#### Create a conda environment

There is no unique way to create a conda environment, we illustrate here how to do so from a .yaml file (see the conda [documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-from-an-environment-yml-file) for more details).

In order to create an environment called `test` with `python=3.6` and `numpy` and `pandas` in it, create `example.yaml`:
```bash
name: test
dependencies:
  - python=3.6
  - numpy
  - pandas
```

Then run the following command: `conda env create -f example.yaml`.

If successful, you should see `test` when listing your environments: `conda env list`. 
You can now activate your environment and use it: `conda activate test`. To double-check that you have the right packages, you can type `conda list` once in the environment and check that you see `numpy` and `pandas`.


### Singularity

For a detailed explanation of how to use Singularity on SDF, you can go through Yee-Ting Li's presentation [here](https://confluence.slac.stanford.edu/display/AI/AI+Seminar#AISeminar-Containers!Containers!Containers!) where you can find both the slides and the zoom recording.

#### Prerequisite

Before pulling or building an image, define the following environment variables:
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


