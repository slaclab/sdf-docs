# Conda

[Conda](https://docs.conda.io/projects/conda/en/latest/index.html) and other Python package management tools such as [UV](https://docs.astral.sh/uv/) and [Poetry](https://python-poetry.org/) allow for easier installation and deployment of Python applications with complex dependencies. The following guide covers common usage patterns for Conda on S3DF.

## Conda Deployment Methods

### Facility installation of Miniconda

An S3DF facility (https://s3df.slac.stanford.edu/#/contact-us?id=poc) typically maintains software deployments relevant to its users under a path in that facility's group space, such as `/sdf/group/<facility>/sw`. The computing czar for a facility, and those they grant permissions to, can install/manage software such as Conda under that facility's group space.

Miniconda is a minimal distribution of Anaconda that contains Python, Conda, their dependencies, and some other useful packages. It is lightweight and has a smaller footprint than a full-fledged Conda or Anaconda deployment. Maintainers can download [Miniconda](https://docs.conda.io/en/latest/miniconda.html) and follow the [installation instructions](https://conda.io/projects/conda/en/latest/user-guide/install/linux.html#installing-on-linux) guide. The installation path can be overridden to point to an appropriate path under the facility group space as follows (replace `<facility>` with the name of the appropriate S3DF facility):

```bash
$ wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O /tmp/Miniconda3-latest-Linux-x86_64.sh
$ bash /tmp/Miniconda3-latest-Linux-x86_64.sh -p /sdf/group/<facility>/sw/conda/
```

Users can add the newly-installed Conda binary to their `$PATH` environment variable by running:

```bash
$ export PATH=${PATH}:/sdf/group/<facility>/sw/conda/bin
```

## Conda Environments

The most common use case for Conda is to resolve and manage Python application dependencies. [Conda environments](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html) allow Python applications to have their own installation environments isolated from each other, with the goal of reducing conflicts between applications that require different versions of the same packages. Users can invoke the environment that has the dependencies required for a specific Python application and run the application within that environment, in isolation from other applications.

Deploying Conda environments requires the following:
* Access to a `conda` binary executable
* Filesystem permissions to write to the directory where the Conda environment(s) will be stored
* Access (usually over the network) to any Python package repositories required (e.g., [the Python Package Index (PyPI)](https://pypi.org/) for the application
* Sufficient disk space in the env location to store the package artifacts

### Creating a Conda environment

Users can modify their individual Conda startup configuration file to set the default Python package channels, any packages, and override the default install path for new Conda envs, among other settings (for a complete list, see: https://conda.io/projects/conda/en/latest/user-guide/configuration/use-condarc.html). The following example configures Conda envs to:

* use the `defaults`, `anaconda`, `conda-forge`, and `pytorch` channels to access Python packages
* sets the environment to be installed under the `envs` directory of the facility's Conda instance
* sets the packages downloaded for environments to be installed under the `pkgs` directory of the facility's Conda instance
  
```bash
$ cat ~/.condarc
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

Conda environments can be created declaratively using YAML files (see: https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-from-an-environment-yml-file).

The following YAML manifest generates a Conda environment called `mytest` with these packages and their dependencies pre-installed:

* `python=3.12` 
* `numpy`
* `pandas`
  
```bash
$ cat mytest-env.yaml
name: mytest
dependencies:
  - python=3.12
  - numpy
  - pandas
```

Create the Conda environment:
```
$ conda env create -f mytest-env.yaml
```

Once created, the `mytest` env should appear when listing Conda environments (`<facility>` is a placeholder): 
```
$ conda env list
# conda environments:
#
base          /sdf/group/<facility>/sw/conda 
mytest        /sdf/group/<facility>/sw/conda/envs/mytest
``` 

The Conda environment may be activated by running: 
```
$ conda activate mytest
```

Once the environment has been activated, the installed package list can be seen by running: 
```
(mytest) $ conda list
# packages in environment at /sdf/group/<facility>/sw/conda/envs/mytest:
#
# Name                    Version                   Build      Channel
[...]
numpy                     2.1.0           py312h58c1407_1      conda-forge
[...]
pandas                    2.2.2                    pypi_0      pypi
[...]
python                    3.12.5          h2ad013b_0_cpython   conda-forge
[...]
```
Note that the package list will show not only the pre-defined packages from the environment's YAML manifest, but any dependencies installed along with them.

Existing Conda environments can be exported into YAML manifests by running the following (change the name of the environment YAML file as desired):
```
$ conda env export > my-existing-env.yaml
```

> [!Note]
> Conda environments should not be stored in the user $HOME directory due to quota limits (30GB per user) and the inability to share the environment with other users. It is recommended to install Conda and other software into the appropriate facility group space (e.g., `/sdf/group/<facility>/sw` - please see [facility storage](getting-started.md#group)). To obtain proper filesystem permissions, please consult with the appropriate facility computing czar. The list of czars for S3DF facilities can be found at: https://coact.slac.stanford.edu/facilities.

## Containerizing Conda environments

Conda environments are designed to isolate a Python application and its dependencies. However, scientific applications frequently have a large number of heavyweight dependencies (e.g., `numpy` and `pandas`) that can utilize a large amount of disk space, as well as needing to be built against specific platforms and architectures for compatibility and performance. Additionally, re-deploying a Python application and its accompanying dependencies within a Conda environment to other systems (e.g., deploying the same application to SLAC and NERSC) can be time-consuming and lead to future maintenance issues as different deployments fall out of sync. Containerization (see: https://aws.amazon.com/what-is/containerization/) allows for the creation of an image that contains a full application stack all the way down to the operating system, which can be run on systems using a compatible container runtime such as `Docker`, `Podman`, `Apptainer`, etc. A Python application, with its accompanying Conda environment, Python packages, and the Conda installation itself, can be built into a container image. This can offer much more portability, especially when running applications in multiple high performance compute environments such as S3DF.

### Creating Container Images

Container images can be built with a variety of tools in different container image formats, e.g. `Dockerfile` or Apptainer Definition files (`.def`), it is recommended to use a format that conforms to the [Open Container Initiative (OCI)](https://opencontainers.org/) standard for both portability and compatibility with the available userspace container runtime on S3DF ([Apptainer](https://apptainer.org/)). Docker images are supported by most container runtimes including Apptainer, thus allowing the container images to be used at multiple compute facilities.

Due to the fact that Docker's container build utility (e.g. `docker build...`) requires admin privileges on the host build system, users must create their Docker container images on a non-S3DF host where they have admin privileges (e.g. a work laptop with `sudo` privileges). Once built, the container image can be uploaded to an online container repository such as [GitHub Container Registry (ghcr.io)](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry), and pulled onto S3DF using the Apptainer container runtime. The following diagram shows the development lifecycle for an application container used on S3DF:


> [!NOTE]
> The host system platform and architecture where a container image is built may differ from the platform and architecture where the container is run. For example, container images can be built on a MacOS or Windows host system, while S3DF batch nodes are on RHEL8/Rocky Linux 8 (and will be migrated to Rocky Linux 9). Docker and other container build tools can be configured to target different platforms and architectures, so ensure that the built container image is compatible with the platform and architecture on S3DF nodes. For more information, see: https://docs.docker.com/build/building/multi-platform/.

> [!WARNING]
> DockerHub repositories are *PUBLIC* by default, so your container images will be visible by anyone on the internet. Be sure to make a private repo if needed, but doing so will require authentication when pushing/pulling images to/from DockerHub.

Once an appropriate repo has been created (e.g. `docker.io/<username>/<repo>`), a Docker image can be built with a Dockerfile:
```
$ cat Dockerfile
FROM continuumio/miniconda3:latest

WORKDIR /app

COPY mytest-env.yaml .

RUN conda env create -f /app/mytest-env.yaml && conda clean -afy

ENV PATH=/opt/conda/envs/test-env/bin:$PATH

CMD ["python"]
```

To build the container image, run the command:

```
$ docker build -t <username>/<repo> .
```

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
> Container images are immutable and must be rebuilt any time changes are needed in the Conda environment.
