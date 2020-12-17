# Software



!> Please note that we are effectively treating the design and implementation of SDF as a green field deployment. As such certain technologies and tools may not be available. Please [contact us](contact-us.md) if you wish for anything to be added or removed.

## I Need Software X...

### Environment Modules

#### SDF Provided Modules

#### Adding Your Own Modules


## Where Do I Install Software?

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


