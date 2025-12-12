# Conda

[Conda](https://docs.conda.io/projects/conda/en/latest/index.html) and other Python package and dependency management tools such as [UV](https://docs.astral.sh/uv/) and [Poetry](https://python-poetry.org/) allow for easier installation and deployment of Python applications with complex dependencies. The following guide covers common usage patterns for Conda on S3DF.

## Conda environments

[Conda environments](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html) are similar to Python [virtual environments](https://docs.python.org/3/library/venv.html). Both allow for the isolation of dependencies for Python application(s) such that multiple environments can install different versions of the same package without conflicting with each other. Users can invoke the environment with the desired dependencies required for a specific Python application and run it within that environmental context, in isolation from other applications outside the loaded environment.

Utilizing Conda environments requires the following:
* Access to a `conda` binary executable
* Filesystem permissions to write to the directory where the Conda environment(s) will be stored
* Sufficient disk space in the env location to store the package artifacts

> [!Note]
> Conda environments should not be stored in the user $HOME directory due to quota limits (30GB per user) and the inability to share the environment with other users. It is recommended to install Conda and other software into the appropriate facility group space (e.g., `/sdf/group/<facility>/sw` - please see [facility storage](getting-started.md#group)). To obtain proper filesystem permissions, please consult with the appropriate facility computing czar. The list of czars for S3DF facilities can be found at: https://coact.slac.stanford.edu/facilities.

## Deploying Conda

### Option 1) Installing Miniconda to group space

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

> [!TIP]
> This Miniconda installation should be used for an entire facility with conda environment(s) installed for the various facility users. Conda installations and packages can be quite large, so they are not recommended to be placed in $HOME.

### Create a Conda environment

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

You can now activate your environment and use it: `conda activate mytest`. To double-check that you have the right packages, you can type `conda list` once in the environment and check that you see `numpy` and `pandas`.

Additionally, existing conda environments can be exported into yaml-formatted files with `conda env export > my-existing-env.yaml`.

## Option 2) Create and invoke a Conda container on S3DF using the Apptainer container runtime

### Docker/OCI images

Due to the fact that Docker's container build utility (e.g. `docker build...`) requires admin privileges on the host build system, users must create their Docker/OCI container images on a non-S3DF host where they have admin privileges (e.g. a work laptop with sudo access).upload the image to a repository such as [GitHub Container Registry (ghcr.io)](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry), then pull the remotely hosted container image onto S3DF with the Apptainer container runtime. Docker/OCI images are supported by most container runtimes, thus allowing portability to use the same container image at multiple compute facilities.

To begin, install docker on your local machine (not S3DF) by visiting the [Docker homepage](https://www.docker.com/get-started). Additionally, sign up for a free Docker Hub account if an online repository is needed.

> [!TIP]
> To build a docker container on a Windows system, consider installing WSL2 (Windows Subsystem for Linux 2) first and then have Docker Desktop link to your WSL2 distribution. Then use docker commands from within WSL2 to ensure container compatibility since S3DF runs on a Linux system.

> [!WARNING]
> Docker Hub repositories are *PUBLIC* by default, so your container images will be visable by anyone on the internet. Be sure to make a private repo if needed, but doing so will require authentication when pushing/pulling images to/from Docker Hub.

Once an appropriate repo has been created (e.g. `docker.io/<username>/<repo>`), a docker image can be built with a provided Dockerfile:
```
FROM continuumio/miniconda3:latest

WORKDIR /app

COPY mytest-env.yaml .

RUN conda env create -f /app/mytest-env.yaml && conda clean -afy

ENV PATH=/opt/conda/envs/test-env/bin:$PATH

CMD ["python"]
```

> [!NOTE]
> This file must be called `Dockerfile` and is used to build the container in the same directory as the `mytest-env.yaml` file.

To build the container image, run the command:

`docker build -t <username>/<repo> .`

This will build the image within the Dockerfile directory and tag it to the name given by `<username>/<repo>` with the Docker Hub username and repo name created earlier. Custom version tags can be appended as well for version control (e.g. `<username>/<repo>:<tag>`), and if not specified, the default tag is `latest`.

> [!TIP]
> Once the docker container is built, it can be tested/debugged locally with `docker run -it <username>/<repo>` which runs it in interactive mode.

Next, *push* (upload) the docker image to an online repository with the command:

`docker push <username>/<repo>`

This will upload the container image to Docker Hub (or other specified online repository).

Now on S3DF, *pull* (download) the docker container image with Apptainer by using the command:

`apptainer pull docker://<username>/<repo>`

This will create a Singularity image file (.sif) with the automatically generated name based on the repo and tag name: `<repo>_latest.sif`.

Lastly, run the container image with Apptainer with the command:

`apptainer run <repo>_latest.sif`

Based on the configuration of the Dockerfile above, the container will immediately open a python interpreter with the specified conda environment.

### Apptainer

Apptainer can also create Apptainer format container images using Apptainer Definition Files (`.def`). To build a specific Conda environment within a container and run it. In addition to providing a desired Conda enviroment as exampled above in `mytest-env.yaml`, an apptainer definition file specifies the image-building procedure for installing Conda and the desired environment packages. To start, create `mytest-app.def`:
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

This should create the Singularity image file: `mytest-env-image.sif` which contains the desired conda environment settings.

To use this apptainer interactively, simply run:

`apptainer shell mytest-env-image.sif`

which opens a terminal prompt within the image with the conda environment activated. Then, from within the Apptainer shell, running `python` opens a python terminal in the installed conda environment.

Alternatively, the apptainer can be used as an executable to run a desired python script (e.g. `my_script.py`) by using the command:

`apptainer run mytest-env-image.sif python my_script.py`

where the arguments following the .sif image are to be run as code within the container.

> [!TIP]
> Only the Singularity image file (.sif) needs to be provided to other S3DF users as everything is self-contained.

> [!NOTE]
> Container images are immutable and must be rebuilt any time changes are needed in the conda environment.
