# Software

Available software is an important part of the S3DF. It is also an area which has a very broad scope. Whenever possible, S3DF will opt for pre-built, packaged software - e.g. RPMs from various well-known repositories. S3DF also uses Lmod to support software packages installed by other methods. With Lmod, S3DF will support a limited number of software packages widely used by the SLAC communities. S3DF encourages experts from non-SCS to use Lmod to provide, support, maintain and share software tools they build.

## S3DF Centrally-Installed Software

S3DF uses the [Lmod Module](https://lmod.readthedocs.io/en/latest/010_user.html) system to administrate common software packages not found in the usual software repositories.

Please [contact us](contact-us.md) if you would like something installed system-wide. Users groups are encouraged to share their software via Lmod module. We can include modulefiles/directory from user groups to the `module avail` list.

> ℹ️ **A note on OpenMPI:** sdfrome nodes have InfiniBand hardware from Mellanox installed (Mellanox Technologies MT28908 Family [ConnectX-6]). On these nodes, openmpi/4.1.4rc1... (as listed below) from the vendor (Mellanox Inc.) is installed instead of the stock OpenMPI from RedHat. We assume this version of OpenMPI will give better performance since it is from the vendor. But this also means we can not install some of the other RedHat/EPEL rpms that were compiled with the stock OpenMPI (e.g. hdf5-openmpi). 

## Communities' Installed/Supported Software via Lmod

S3DF encourages groups to use to Lmod to manage, support and maintain their software tools, for their own groups, or share with other groups. S3DF can help include those software tools in the Lmod tools. In most cases, SCS will have no knowledge of those software tools, and will not be able to support and maintain them.

Non-general purpose software should be installed locally by you under $HOME or project directories. The latter is preferred as your home space is limited and the project space offers better visibility to a larger audience.

## Lmod
### Common Lmod commands
The `module` command is used to work with Lmod modules. It has a number of subcommands. Below is a selection of the most essential subcommands. Use `module help` to get the full list.

#### Finding modules
##### Listing available modules
`module avail` (or `module av`) displays a list of all modules currently avaiable, grouped by each directory of modulefiles. Modules that are already loaded are marked with `(L)`.

```
❯ module av

------------------------------- /etc/modulefiles -------------------------------
   slurm (L)

---------------------------- /usr/share/modulefiles ----------------------------
   mpi/mpich-x86_64    mpi/openmpi-x86_64 (D)    pmi/pmix-x86_64

----------------------- /sdf/group/cryoem/sw/modulefiles -----------------------
   cryosparc/4.4.1+240110          motioncor2/1.4.5    relion/ver5.0 (D)
   cryosparc/4.4.1+240110-3 (D)    openmpi/v5.0.4
   ctffind/4.1.14                  relion/ver4.0

----------------------------- /sdf/sw/modulefiles ------------------------------
   hdf5/mpich-EPEL         matlab/R2022b
   intel/2020.4.304        mysql/mysql8.0.30
   intel/mpi/2020.4.304    openmpi/v4.1.6
   kubectl/1.30.3          openmpi/4.1.4rc1-gcc-8.5.0-Mellanox (D)
   kubens/kubectx/0.9.5    osg/client-latest
   kubeutils/1.0.0         vault/1.17.3
   kustomize/5.4.3         xq/1.2.4
   maplesoft/maple2023     yq/4.44.3

  Where:
   L:  Module is loaded
   D:  Default Module
```
##### Searching modules
`module keyword <keyword>` (or `module key <keyword>`) searches for any module that contains the given keyword.

`module spider <module name, keyword, string...>` searches available modules for the given string, keyword, etc.

`module -r <keyword, spider, avail, list> <regex>` enables regular expression filtering for the subcommand.

#### Getting information about a module
`module whatis <module name>` gives addtionaly information about a module, including version, brief description, and link to documentation.

#### Using modules
`module load <module name>` loads the given module. A specifc version of the module is loaded with `<module name>/<version>`.
`module unload <module name>` unloads the given module.
`module purge` unloads *all* modules.
`module update` reloads all currently-loaded modules.

## Other Software Info

Remember to check out the "Reference" section for more info about software.
