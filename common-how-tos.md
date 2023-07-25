# Common How-to's
## Build and run MPI jobs
1. **Choose an interactive node that supports your MPI environment.** We recommmend (re)compiling your programs using the same MPI library versions that exist on the S3DF clusters. The RHEL-supplied OpenMPI 4.x distro is installed on all Milan cluster nodes (milano partition) and the "iana" interactive pool. Once you are logged into an iana node, you load the RHEL OpenMPI shell environment via the `mpi/openmpi-x86_64` module. 
