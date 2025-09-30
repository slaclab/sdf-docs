# Build and Run MPI Jobs


## Choose an interactive node that supports your MPI environment

We recommmend (re)compiling your programs using the same MPI library versions that exist on the S3DF clusters. The RHEL-supplied OpenMPI 4.x distro is installed on all Milan cluster nodes (milano partition) and the "iana" interactive pool. Once you are logged into an iana node, you load the RHEL OpenMPI shell environment via the `mpi/openmpi-x86_64` module. 
```
[yemi@sdfiana006 ~]$ module load mpi/openmpi-x86_64
[yemi@sdfiana006 ~]$ which mpirun
/usr/lib64/openmpi/bin/mpirun
[yemi@sdfiana006 ~]$ mpirun -V
mpirun (Open MPI) 4.1.1
```

## Compile on the Interactive Node

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

## Create the Slurm job Submission Script

SLURM will schedule our MPI program to run on the milano partition using the same MPI environment we compiled with:

```
#!/bin/sh
#SBATCH --partition=milano
#SBATCH --ntasks-per-node=4
#SBATCH --nodes=4
module load mpi/openmpi-x86_64
mpirun /sdf/home/y/yemi/slurmtests/openmpi_4.1.1/my_mpi_reduce
```

## Launch the Job

```
[yemi@sdfiana006 openmpi_4.1.1]$ sbatch ./mpi_milano_test.sh
Submitted batch job 20061888
```

## Python MPI Code

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