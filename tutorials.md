# Tutorials
## Build and run MPI jobs
**Choose an interactive node that supports your MPI environment**

We recommmend (re)compiling your programs using the same MPI library versions that exist on the S3DF clusters. The RHEL-supplied OpenMPI 4.x distro is installed on all Milan cluster nodes (milano partition) and the "iana" interactive pool. Once you are logged into an iana node, you load the RHEL OpenMPI shell environment via the `mpi/openmpi-x86_64` module. 
```
[yemi@sdfiana006 ~]$ module load mpi/openmpi-x86_64
[yemi@sdfiana006 ~]$ which mpirun
/usr/lib64/openmpi/bin/mpirun
[yemi@sdfiana006 ~]$ mpirun -V
mpirun (Open MPI) 4.1.1
```
**Compile on the interactive node**

Here's a simple reduction program "my_mpi_reduce.c" that sums the values across all the MPI ranks:

```
#include <stdio.h>
#include <mpi.h>

int main(int argc, char *argv[]) {
  int rank,  value, global_sum, namelen;
  char processor_name[MPI_MAX_PROCESSOR_NAME];

  MPI_Init(&argc, &argv);
  MPI_Comm_rank(MPI_COMM_WORLD, &rank);
  MPI_Get_processor_name(processor_name, &namelen);
  
  value = (rank +1) * 10;
  printf("rank %d on %s has value %d\n",rank,processor_name,value);

  MPI_Reduce(&value, &global_sum, 1, MPI_INT, MPI_SUM, 0,MPI_COMM_WORLD);
  if(rank == 0){
    printf("Rank 0 worked out the total %d\n",global_sum);
  } 

  MPI_Finalize();
}
```

Using the supplied MPI compiler from `mpi/openmpi-x86_64` :

```
[yemi@sdfiana006 openmpi_4.1.1]$ which mpicc
/usr/lib64/openmpi/bin/mpicc
[yemi@sdfiana006 openmpi_4.1.1]$ mpicc -o my_mpi_reduce my_mpi_reduce.c
```
**Create the SLURM job submission script**

SLURM will schedule our MPI program to run on the milano partition using the same MPI environment we compiled with:

```
#!/bin/sh
#SBATCH --partition=milano
#SBATCH --ntasks-per-node=4
#SBATCH --nodes=4
module load mpi/openmpi-x86_64
mpirun /sdf/home/y/yemi/slurmtests/openmpi_4.1.1/my_mpi_reduce
```
**Launch the script**

```
[yemi@sdfiana006 openmpi_4.1.1]$ sbatch ./mpi_milano_test.sh
Submitted batch job 20061888
```
**Python MPI code**

Python MPI programs typically use the mpi4py module. At this time, S3DF is not supporting python centrally. This is because each project has their own python distribution with scripts for configuring their environment. Here's an example of a python MPI job submission script

```
#!/bin/sh
#SBATCH --partition=milano
#SBATCH --ntasks-per-node=2
#SBATCH --nodes=2
# "-u" flushes print statements which can otherwise be hidden if mpi hangs
# "-m mpi4py.run" allows mpi to exit if one rank has an exception
source /sdf/group/<facility>/..../bin/psconda.sh
mpirun python -u -m mpi4py.run ~/slurmtests/my_mpiReduce.py
``` 
## S3DF Migration Guide

**Am I entitled to use the S3DF?**

 If your computing tasks are associated with SLAC research or engineering, you should use the S3DF. It is fully supported by the lab. The first step is to identify the context of your work by selecting an S3DF ‘Facility’ - we use this term to describe an experiment, project or facility that has a user group and resource requirements. Every S3DF user is a member of a facility. Every facility has czars that act as gatekeepers and are authorized to manage any resources belonging to a facility.

**Accounts and Authentication**

S3DF uses central SLAC Unix accounts and UIDs. Password authentication is via central SLAC Kerberos. If you don’t have a SLAC Unix account, you can request one from the SLAC IT Helpdesk. Our long term goal is to eventually use Federated Identity login. This will allow users to authenticate to their SLAC Unix account using a password service from an external provider such as Stanford Campus or another institution.

**What is Coact?**

[Coact](http://coact.slac.stanford.edu) is our portal for managing authorizations and tracking resource utilization. The czars control who gets access and how facility resources are distributed. Every new S3DF user must first login to coact (using their Unix account) and request S3DF access by specifying a facility. The facility czar must then approve the request before the user can login.

**Login vs Interactive pools**

SSH login access to S3DF is via the ```s3dflogin.slac.stanford.edu``` pool. These systems are designed as externally-facing “bastion” login nodes. They only mount user home directories and they run a limited number of commands. Once users have gained access via the login pool, they should then SSH into an [interactive pool](interactive-compute). Several facilities have their own dedicated interactive hosts but all users can access the ‘iana’ pool. Use the interactive systems for interactive applications, compilation, slurm cluster commands, etc.

**Primary vs Legacy Filesystems** 

S3DF primary filesystems are mounted ( under ```/sdf``` ) on all S3DF interactive and compute hosts. This includes S3DF home directories, per-facility “group” space and multi-petabyte storage for the bulk of science data. These primary filesystems will eventually replace all legacy SLAC storage. The DDN Lustre storage from SDF “1.0” is also mounted across all S3DF interactive and compute, under ```/fs/ddn/sdf``` . Several facilities invested in 5 years of DDN storage - we will honor this investment. Legacy filesystems (GPFS, NFS) have already surpassed the 5 year lifecycle. To help migrate data off legacy storage, we have mounted a select number of GPFS filesystems on the interactive nodes. AFS is also mounted read-only on interactive nodes. See [data and storage](data-and-storage.md).

**What is the future of AFS?**

AFS will be retired in June 2024, along with other RHEL6 infrastructure and platforms. Our goal is for S3DF native storage to be securely exported to test stands, control rooms, lab workstations, etc via authenticated NFS v4. Before we shutdown AFS, we will take a final copy of the entire “/afs/slac” directory tree and make select portions of it available read-only for a limited period of time. This will allow groups to copy data they may have forgotten to migrate earlier.

**Is there any ‘free’ S3DF Storage?**

All S3DF users get a home directory with a 25GB quota. There is also S3DF /sdf/group space with per-facility quotas. The group space is intended for project-specific software, configuration files, etc. Typically, each facility has an /sdf/group quota of 10TB. Home directories and group space are stored on flash (NVMe SSDs) and are backed up to tape. We also provided shared scratch space for free (limited lifetime and not backed up) with a quota of 100GB. The bulk of science data (PB scale) is funded directly by the facilities and located in /sdf/data. We have a business model and the facility czars purchase their storage hardware for science data.

**Transferring files and data**

S3DF has inherited the POSIX groups that are used for legacy storage permissions. This means S3DF users should have consistent file ownership and permissions, allowing them to copy over existing files from legacy to S3DF primary filesystems. If you are unable to copy your groups’ data because you lack the permissions, please contact s3df-help@slac.stanford.edu. We have administrator-level access to all central legacy storage. [For external transfers over the internet, we provide a pool of Data Transfer Nodes](data-transfer.md#data-transfer) . 

**Compiling code for S3DF**

The standard Linux distro for all S3DF machines is RHEL 8.6. We recommend you port your codes and applications to RHEL 8. You can compile on our interactive nodes or submit build jobs to our clusters. We are also looking at incorporating Rocky Linux 9 (a RHEL clone) into our environment.

**Where to find libraries and packages**

We are keeping the quantity of locally installed packages (on a host’s local disk filesystem) to a minimum. Contact us if you are missing “core” HPC packages and we’ll consider installing RPMs from the default yum repos (Examples: BLAS, LAPACK, etc). A more flexible method of distributing software is to install it on our S3DF filesystems that are mounted on all hosts. We can install general packages under ```/sdf/sw``` . Facilities can keep their specific packages under ```/sdf/group/<facility>/```

**Exporting your software environment**

S3DF uses the popular lmod module system for configuring shell environments. We can update modulefile search paths to include subdirectories under ```/sdf/sw/``` or ```/sdf/group/<facility>/``` . 

**Web applications and HTML content**

We are hosting dynamic web applications and static content. Please see [service-compute.md#s3df-dynamic-sites-and-web-applications] . We are also discussing how to preserve existing AFS public_html directories that are accessed world-wide via ```https://www.slac.stanford.edu/~<username>``` . 

**Cron Jobs**

We now have an [S3DF Cron Service](service-compute.md#?s3df-cron-tasks)

## Graphics and remote visualization
**Introduction to NoMachine**

NoMachine is the recommended (supported) interface for displaying and interacting with graphics-based programs running on S3DF. The NoMachine "NX" protocol offers improved performance compared to X11 over SSH encryption.  It is located at s3dfnx.slac.stanford.edu.
