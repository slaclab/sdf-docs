# Software

Available software is an important part of the S3DF. It is also an area which has a very broad scope. Whenever
possible, S3DF will opt for pre-built, packaged software, e.g. RPMs from various well known repos. S3DF also uses
Lmod to support software that are installed in other methods. 

With Lmod, S3DF will centrally support a limited number of software that are both widely used by the SLAC 
communities, and are understandable/maintainable by the SCS administrators. S3DF encourages experts from 
non-SCS to use Lmod to provide, support, maintain and share software tools they build.   

## S3DF Centrally Installed Software

S3DF uses the module system (Lmod). Currently installed modules can be viewed
with this command: `module avail`


To load a specific module (and use the software), use the `module load module-name-you-want` command.

```
--------------------------------------------------- /etc/modulefiles ---------------------------------------------------
   slurm (L)

------------------------------------------------ /usr/share/modulefiles ------------------------------------------------
   mpi/mpich-x86_64

------------------------------------------------- /sdf/sw/modulefiles --------------------------------------------------
   hdf5/mpich-EPEL    intel/2020.4.304    intel/mpi/2020.4.304    openmpi/4.1.4rc1-gcc-8.5.0-Mellanox

  Where:
   L:  Module is loaded
```

[Contact us](contact-us.md) if you would like something installed system wide. Users groups are encouraged to share their software via module / Lmod. We can include modulefiles/directory from user groups to the `module avail` list.

A note the OpenMPI: sdfrome nodes have InfiniBand hardware from Mellanox installed (Mellanox Technologies MT28908 Family [ConnectX-6]). On these nodes, openmpi/4.1.4rc1... (as listed above) from the vendor (Mellanox Inc.) is installed instead of the stock OpenMPI from RedHat. We assume this version of OpenMPI will give better performance since it is from the vendor. But this also means we can not install some of the other RedHat/EPEL rpms that were compiled with the stock OpenMPI (e.g. hdf5-openmpi). 

## Communities Installed/Supported Software via Lmod

S3DF encourages other groups to use Lmod to manage, support and maintain their software tools, for their own groups,
or share with other groups. S3DF can help include those software tools in the Lmod tools. In most cases, SCS will 
have no knowledge of those software tools, and will not be able to support and maintain them.

## Other Software Info

Remember to check out the "Reference" section for more info about software.
